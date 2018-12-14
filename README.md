[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-AndroidYoutubeOverlay-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/1324)


AndroidYoutubeOverlay
=====================

Library for handling Youtube Player in scrollable Views (ListView, GridView, ScrollView...)

Features:
---------

* Allows seamless transition between portrait and landscape (without rebufering)
* Allows playback of one video at time
* Attaches it self to view in scrollable container and scrolls with it
* Supports AbsListView and ScrollView
* Works from API level 17 (like YT API)

Todo:
-----

* Test with Horizontal ScrollView
* Added Touch event passing to underlying scrollable View
* Added RecyclerView support

How to Use:
-----------

- Add following line to Activity declaration in AndroidManifest.xml, which will handle YT playback
```
  android:configChanges="orientation|keyboardHidden|screenSize"
```

- Use builder to create Fragment instance (Remember to set proper YT_DEVELOPER_KEY for your own project)
```
    ytPlayer = YoutubeOverlayFragment.newBuilder(YT_DEVELOPER_KEY, this).setListId(SCROLLABLE_CONTAINER_ID).buildAndAdd();
```

- Handle view click in your adapter getView()
```
    @Override
    public View getView(final int position, View convertView, ViewGroup parent) {
        (...)
        final String videoId = getItem(position);
        holder.rowMainImage.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                ytPlayer.onClick(holder.rowMainImage, videoId, position);
            }
        });
        return convertView;
    }
```

- Or in your ScrollView
```
  @Override
  protected void onCreate(Bundle savedInstanceState) {
        (...)
      final View img = findViewById(R.id.rowMainImage);
      img.setOnClickListener(new View.OnClickListener() {
          @Override
          public void onClick(View v) {
              ytPlayer.onClick(img, VIDEO_ID);
          }
      });
  }
```

- Override onBackPressed, so fragment can handle back button while in landscape
```
  @Override
  public void onBackPressed() {
      if (ytPlayer.onBackPressed()) {
          // handled by ytPlayer fragment
      } else {
          super.onBackPressed();
      }
  }
```

### Support:

If you want the good work to continue please support us on

* [PAYPAL](https://www.paypal.me/ishandutta2007)
* [BITCOIN ADDRESS: 3LZazKXG18Hxa3LLNAeKYZNtLzCxpv1LyD](https://www.coinbase.com/join/5a8e4a045b02c403bc3a9c0c)
