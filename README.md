# ReactNative-Adaptive-Splash-Screen-Android

 ### This project demonstrates how to build a splash screen which adapts according to screen orientation (landscape/portrait) in your ReactNative Project in Android.

Setup:-

1) Create a `drawable` and `drawable-land` folder for landscape and portrait mode respectively in the `res` directory.

2) Put your splash screen Images for portrait mode in `drawable` folder.

3) Put your splash screen Images for landscape mode in the `drawable-land` folder, 
make sure its name must be same as splash screen image of drawable folder.

4) Include Glide Image Loading Lib in your dependency path. Using Glide for Splash Screen loading will make ensure that the app won't throw OOM exception in devices with low memory. 
GLide also handle caching of images so next time image will load faster. Also, glide allows you to load Gifs.

5) Next, create a `SplashActivity` Class with a layout file of your choice. Here I am using an Image as background with a title and Slogan in center of the screen.

6) Load your Splash images into splash screen layout with the help of Glide. Start the actual app after some time ideally it should be 800mS.

      public class SplashActivity extends AppCompatActivity {

          public static final int DELAY_MILLIS = 800;

          @Override
          protected void onCreate(Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              requestWindowFeature(Window.FEATURE_NO_TITLE);
              getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);
              setContentView(R.layout.activity_splash);
              Glide.with(SplashActivity.this)
                      .load(R.drawable.splash_bg)
                      .centerCrop()
                      .crossFade()
                      .into((ImageView) findViewById(R.id.splash_background));

              new Handler().postDelayed(new Runnable() {
                  @Override
                  public void run() {
                      startActivity(new Intent(SplashActivity.this, MainActivity.class));
                      overridePendingTransition(android.R.anim.fade_in, android.R.anim.fade_out);
                      finish();
                  }
              }, DELAY_MILLIS);

          }
      }

