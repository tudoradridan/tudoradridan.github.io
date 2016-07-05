---
layout: post
title: (Android)Check internet access to before connecting to server
---
Every app need to access a server. It's nice to check if we can connect to that server before we actually do it.
We have two ways to do that.

# Simple way, check if we are connected

What this means? It tells us that we are connected to a WiFi Router **or** our Cellular Data are active and we are connected to a Radio Base Station(2G/3G/4G).

```java
public static boolean isNetworkConnected(Context context) {
		ConnectivityManager cm = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
		NetworkInfo ni = cm.getActiveNetworkInfo();
		return (ni != null && ni.isConnectedOrConnecting());
	}
```
Check if you have this in AndroidManifest.xml

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

# Hard way, check if we can access the server

The ugly part here is that we must call this insinde an AsyncTask, otherwise will get an NetworkOnMainThreadException. But this can assure us that the resource we are requesting exists.

```java
public static final boolean isInternetOn(Context myContext) {

		try{
			URL url = new URL("http://www.google.com");
			HttpURLConnection connection = (HttpURLConnection) url.openConnection();
			connection.setRequestProperty("User-Agent", "yourAgent");
			connection.setRequestProperty("Connection", "close");
			connection.setConnectTimeout(2000);
			connection.connect();

			if (connection.getResponseCode() == 200) {
				return true;
			}
		}
		catch (Exception e) {
			e.printStackTrace();
			return false;
		}
		return false;
	}
```
#Another way

```java
public static Boolean isServerUp(){
  String ip = "serverIp"
  Integer port = "serverPort"
  Socket s = null;
	try {
		s = new Socket(serverIp, serverPort);
		return true;
	} catch (Exception e){
		return false;
	} finally {
		if (s != null)
			try {
				s.close();
			} catch (Exception e) {
			}
	}
}
```

There is no silver bullet. Choose the one that fits your needs.
