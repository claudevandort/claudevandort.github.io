---
layout: post
title:  "Fetching data from the Net"
date:   2017-08-16 20:40:00 -0300
categories: android internet
---
# Starting
What we're intending to do here, is to hit a public endpoint that returns data as json, then parse the response and show it in our app. To illustrate this we're gonna hit a public Github Search endpoint.

To start we create a project with a blank activity. Then on the layout we're going to place an EditText element which will contain our query to the github service, a TextView to show the url we're aiming to, and another TextView to show the Github's response, and to be able to scroll through the response we're gonna wrap this last TextView on a ScrollView as follows.

activity_main.xml
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_height="match_parent"
    android:layout_width="match_parent"
    android:orientation="vertical"
    android:paddingLeft="16dp"
    android:paddingRight="16dp"
    android:paddingTop="16dp">
    <EditText
        android:id="@+id/search_query_edit_text"
        android:hint="Type Github query"
        android:textSize="22sp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
    <TextView
        android:id="@+id/url_text_view"
        android:hint="URL will show here"
        android:textSize="22sp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <TextView
            android:id="@+id/response_text_view"
            android:textSize="18sp"
            android:hint="Results will show up here"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
    </ScrollView>
</LinearLayout>
{% endhighlight %}

# Submit menu button
Yes, we're gonna place our submit button on the action bar.. because we can, and so we can get a glimpse on how menus work.

First we're defining the text of the button in the strings.xml file.
{% highlight xml %}
<string name="search">Search</string>
{% endhighlight %}

Then we create the menu by adding the resource file res/menu/main.xml:
- Right click on res, then new, then Android resource directory, then resource type: menu, then ok.
- Right click on menu, then new, then Menu resource file, then ok.

Then on main.xml we should have
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/action_search"
        android:title="@string/search"
        app:showAsAction="ifRoom"
        android:orderInCategory="1"></item>
</menu>
{% endhighlight %}

# Get response from the Net
Now that we have our layout ready we can start to make things work. Now we need to grab the search query from the EditText we made earlier and with it build the URL we're going to hit, then with it make a request, fetch the results and display them in the TextView we made for that end.

We're going to start by making the class that will help us to make the request to a URL and get the result.

NetworkUtils.java
{% highlight java %}
public class NetworkUtils {
    public static String getResponseFromHttpUrl(URL url) throws IOException{
        HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
        try{
            InputStream inputStream = urlConnection.getInputStream();

            Scanner scanner = new Scanner(inputStream);
            scanner.useDelimiter("\\A");

            if(scanner.hasNext())
                return scanner.next();
            else
                return null;
        }finally {
            urlConnection.disconnect();
        }
    }
}
{% endhighlight %}

Now that we can make requests to the web and get the results, we need to build the url and execute the request to query github. Given that a request to the web might take an unknown amount of time, our app would freeze if we execute it in the main thread, so we need to do it in a background thread.

To accomplish this we're going to use the construct AsyncTask which is a quite simple abstraction to use threads. We're going to declare the AsyncTask inside the MainActivity class as follows.
{% highlight java %}
public class GithubQueryTask extends AsyncTask<String, Void, String>{
    final static String GITHUB_BASE_URL = "https://api.github.com/search/repositories";
    final static String PARAM_QUERY = "q";
    final static String PARAM_SORT = "sort";

    @Override
    protected String doInBackground(String... params) {
        String searchQuery = params[0];
        String githubSearchResults = null;
        try{
            githubSearchResults = NetworkUtils.getResponseFromHttpUrl(buildGithubSearchUrl(searchQuery));
        }catch (IOException e){
            e.printStackTrace();
        }
        return githubSearchResults;
    }

    @Override
    protected void onPostExecute(String s) {
        if(s != null && !s.equals("")){
            mResponseTextView.setText(s);
        }
    }

    public Uri buildGithubSearchUri(String query){
        return Uri.parse(GITHUB_BASE_URL).buildUpon()
                .appendQueryParameter(PARAM_QUERY, query)
                .appendQueryParameter(PARAM_SORT, "stars")
                .build();
    }

    public URL buildGithubSearchUrl(String query){
        URL url = null;
        try{
            url = new URL(buildGithubSearchUri(query).toString());
        }catch (MalformedURLException e){
            e.printStackTrace();
        }
        return url;
    }
}
{% endhighlight %}

And last, in the MainActivity class we make the references to our UI elements and handle the search menu button click, to make it execute the task we just made and show the results.
{% highlight java %}
EditText mSearchQueryEditText;
TextView mUrlTextView;
TextView mResponseTextView;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    mSearchQueryEditText = (EditText) findViewById(R.id.search_query_edit_text);
    mUrlTextView = (TextView) findViewById(R.id.url_text_view);
    mResponseTextView = (TextView) findViewById(R.id.response_text_view);
}

@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.main, menu);
    return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    int selectedMenuItem = item.getItemId();
    if(selectedMenuItem == R.id.action_search){
        String githubSearchQuery = mSearchQueryEditText.getText().toString();
        GithubQueryTask task = new GithubQueryTask();
        mUrlTextView.setText(task.buildGithubSearchUrl(githubSearchQuery).toString());
        task.execute(githubSearchQuery);
    }
    return true;
}
{% endhighlight %}
