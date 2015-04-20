# Google Spreadsheets

One really straightforward way to get your app to push data to the cloud in a accessible way (paving toward post-analysis)
is to push directly to a Google spreadsheet.

1) you will need to create a google form with the fields you would like to push.

2) you will need to add the following snippet to your code (e.g. inside a button, or postHandler):

- make this a field of your Activity
```Java
String url;
```

- Place this wehere you want to update the url:
```Java
         double data = 9001; // awesomeness_level
         String form_hash="1QQn0fDwwdnRpLeW9ih_uXlPtWDKVTLpN55haNl-q7-U"; //replace with hash
         Stirng data = "entry.456604062=" + data;
         auto_submit = "&submit=Submit"; //add this to the end to make it autosubmit
         String url = "https://docs.google.com/forms/d/" + form_hash + "/formResponse?" + data + auto_submit;
```

- Using the following line to execute the httprequest:
```Java
  new RequestTask().execute(url);
```

3) add this class to your activity (credit to [Konstantin Burov](http://stackoverflow.com/questions/3505930/make-an-http-request-with-android))
```Java
class RequestTask extends AsyncTask<String, String, String> {

        @Override
        protected String doInBackground(String... uri) {
            HttpClient httpclient = new DefaultHttpClient();
            HttpResponse response;
            String responseString = null;
            try {
                response = httpclient.execute(new HttpGet(uri[0]));
                StatusLine statusLine = response.getStatusLine();
                if(statusLine.getStatusCode() == HttpStatus.SC_OK){
                    ByteArrayOutputStream out = new ByteArrayOutputStream();
                    response.getEntity().writeTo(out);
                    responseString = out.toString();
                    out.close();
                } else{
                    //Closes the connection.
                    response.getEntity().getContent().close();
                    throw new IOException(statusLine.getReasonPhrase());
                }
            } catch (ClientProtocolException e) {
                //TODO Handle problems..
            } catch (IOException e) {
                //TODO Handle problems..
            }
            return responseString;
        }

        @Override
        protected void onPostExecute(String result) {
            super.onPostExecute(result);
            //Do anything with response..
        }
    }
```



:sparkles: As a bonus, all submissions are timestamped :thumbsup:, since all google forms submissions are auto-stamped to the second. :sparkles:
