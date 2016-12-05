## Get Request with HttpURLConnection

``` java
public String doGetRequest(String urlString) throws IOException{
    try {
        URL url = new URL(urlString);
        HttpURLConnection urlConnection = null;
        try {
            urlConnection = (HttpURLConnection) url.openConnection();
            InputStream in = new BufferedInputStream(urlConnection.getInputStream());
            return readStream(in);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            urlConnection.disconnect();
        }
    } catch (MalformedURLException e) {
        e.printStackTrace();
    }
    return null;
```
