# Persona-SDK

### 1. Add library
1. Add **Personaly_x.x.x-release.aar** file to the libs folder of application

2. Add next to the build.gradle of app:

```
apply plugin: 'com.android.application'
apply plugin: 'com.neenbedankt.android-apt'

popallprojects {
    repositories {
        jcenter()
        flatDir {
            dirs project.property("libs")
        }
    }
}

dependencies {
compile(name: 'Personaly_x.x.x-release', ext: 'aar')
}
```

3. Open build.gradle file of project nad add next:

```
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.neenbedankt.gradle.plugins:android-apt:1.8'
    }
}
```

### 2. Test keys:
```
    private final String APP_ID = "58c654dce72cbf1000c735b3";
    private final String USER_ID = "test id";
    private final String CAMPAIGN_PLACEMENT_ID = "58c654dce72cbf1000c735bd";
    private final String OFFER_APP_ID = "8f0378d53ab2c1e7c9d064791da26f43";
    private final String APP_WALL_PLACEMENT_ID = "58c654dce72cbf1000c735b5";
```

### 3. SDK initialization:
```
Persona.init(this, APP_ID, USER_ID);
```
or
```
Persona.InitCallback initCallback = new Persona.InitCallback() {
        @Override
        public void onSuccess() {
            showToast("InitCallback success");
        }

        @Override
        public void onFailure(Throwable throwable) {
            showToast(throwable.getMessage());
        }
    };
Persona.init(this, APP_ID, USER_ID, initCallback);
```

### 4. Optional listener
```
private SimpleAdListener adLoadListener = new SimpleAdListener(){

        @Override
        public void onLoading() {
            showToast("onLoading");
        }

        @Override
        public void onLoaded() {
            showToast("Successfully loaded");
        }

        @Override
        public void onFailed(Throwable throwable) {
            showToast(throwable.getMessage());
        }

        @Override
        public void onComplete() {
            showToast("onComplete");
        }

        @Override
        public void onHide() {
            showToast("VideoAd onHide");
        }

        @Override
        public void onClosed() {
            showToast("onClosed");
        }

        @Override
        public void onShow() {
            showToast("onShow");
        }

        @Override
        public void onClick() {
            showToast("onClick");
        }
    }
```

### 5. Campaign ad: 
```
Persona.CAMPAIGNS.setListener(adLoadListener);
Persona.CAMPAIGNS.loadAd(CAMPAIGN_PLACEMENT_ID);
```
or
```
Persona.CAMPAIGNS.loadAd(CAMPAIGN_PLACEMENT_ID, adLoadListener);

```
If ad is loaded and ready to show - there are several options to show ad:
```
Persona.CAMPAIGNS.show();
Persona.CAMPAIGNS.show(Activity.this);
Persona.CAMPAIGNS.show(1);
```

### 6. Offers ad
Init and show:
```
Persona.OFFERS.setListener(adLoadListener);
Persona.OFFERS.setAppId(OFFER_APP_ID).show();
```

### 7. App Wall ad
Init and show:
```
Persona.APP_WALL.setListener(adLoadListener);
Persona.APP_WALL.setPlacementId(APP_WALL_PLACEMENT_ID);
Persona.APP_WALL.show(MainActivity.this);
```
or
```
Persona.APP_WALL
             .setPlacementId(APP_WALL_PLACEMENT_ID, adAppWallListener)
             .show(MainActivity.this);
```
