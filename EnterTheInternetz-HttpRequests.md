# Internetz

This file shows some basics on how to send & get data the interwebs


## Send only -- HTTP request

Sometimes you just want to submit a form on a website via your app, mira the following example:

This is an example of a class that extends AsyncTask and allows you to send an http request to a site (nothing returned/analyzed in this simple case)

#### Asynchronous HTTP Request

```java
        private class SendInfo extends AsyncTask<Void, Void, Void> {
            @Override
            protected Void doInBackground(Void... params) {
                String baseUrl = "http://www.someexample.com/someform?";
                String item = "pizza";
                String order = "yes please";

                try {
                    HttpClient httpclient = new DefaultHttpClient();

                    String sendUrl = baseUrl
                   +  item + "=" + order + "&"; //copy pasta this line for more key value pairs

                    // make get request
                     httpclient.execute(new HttpGet(sendUrl.replace(" ", "%20")));//remember to replace blank lines appropriately
                     //httpclient.execute(new HttpGet(sendUrl.replace(" ", "+")));//sometimes "+"'s are used, aka google maps
                     
                } catch (MalformedURLException e) {
                    e.printStackTrace();
                } catch (ClientProtocolException e) {
                    e.printStackTrace();
                } catch (IOException e) {
                    e.printStackTrace();
                }

                return null;
            }
        }
```

#### Execution

Now you can execute the code from anywhere (like a button) that has access

```java
new SendInfo().execute();
```

## TODO -- Send and Receive
