
______________Try the code of Custom dialog Box with using Animation...._______

<style name="DialogAnimation_2">
        <item name="android:windowEnterAnimation">@anim/slide_up</item>
        <item name="android:windowExitAnimation">@anim/slide_bottom</item>
</style>

<-----------anim/slideup.xml-------------->

<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:duration="@android:integer/config_mediumAnimTime"
        android:fromYDelta="100%"
        android:interpolator="@android:anim/accelerate_interpolator"
        android:toXDelta="0">
    </translate>
</set>



<------------------slide_bottom.xml----------------->

<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <translate
        android:duration="@android:integer/config_mediumAnimTime"
        android:fromYDelta="0%p"
        android:interpolator="@android:anim/accelerate_interpolator"
        android:toYDelta="100%p">
    </translate>
</set>

<------add merge this code with dialog object in dialog method i does it already ----------->

getWindow().getAttributes().windowAnimations = R.style.DialogAnimation_2;

use this----
dialog.getWindow().getAttributes().windowAnimations = R.style.DialogAnimation_2;

<--------------dilaog_custom.xml------------->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="300dp"
    android:layout_height="wrap_content"
    android:orientation="vertical">
    
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">
        <FrameLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
            <RelativeLayout
                android:id="@+id/ll_picture"
                android:layout_width="match_parent"
                android:background="@drawable/dialog_shape"
                android:layout_height="150dp">
                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:orientation="vertical">
                    <ImageView
                        android:layout_width="40dp"
                        android:layout_height="40dp"
                        android:layout_gravity="center"
                        android:padding="5dp"
                        android:layout_marginTop="10dp"
                        android:src="@drawable/confirm_ic"/>
                    <TextView
                        android:id="@+id/msg1"
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_margin="5dp"
                        android:gravity="center"
                        android:textAppearance="@style/MySerifBold"
                        android:text="hdshdghjsdg"
                        android:textColor="#e4000000"
                        android:padding="10dp"
                        android:textSize="18sp"
                        android:shadowColor="#00ccff"
                        android:shadowRadius="1.5"
                        android:shadowDx="1"
                        android:shadowDy="1" />
                </LinearLayout>
            </RelativeLayout>
            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal"
                android:weightSum="10"
                android:gravity="center"
                android:background="@android:color/transparent"
                android:layout_marginTop="115dp">
                <LinearLayout
                    android:layout_width="0sp"
                    android:layout_height="match_parent"
                    android:gravity="center"
                    android:layout_weight="4">
                    <ImageView
                        android:id="@+id/img_ok"
                        android:layout_width="60dp"
                        android:layout_height="60dp"
                        android:layout_gravity="center_horizontal"
                        android:src="@drawable/ok_btn" />
                </LinearLayout>
                <LinearLayout
                    android:layout_width="0sp"
                    android:layout_height="match_parent"
                    android:gravity="center"
                    android:layout_weight="4">
                    <ImageView
                        android:id="@+id/img_cancel"
                        android:layout_width="60dp"
                        android:layout_height="60dp"
                        android:layout_gravity="center_horizontal"
                        android:src="@drawable/cancel_btn" />
                </LinearLayout>
            </LinearLayout>
        </FrameLayout>
    </LinearLayout>
</LinearLayout>


<-----------------java-- method------------->

and paste it where you want to open dialog box 

 createAlertDouble1(this, "Are you sure want to back Home?", true);

----------------------
 private void createAlertDouble1(final Activity mActivity, String message,  final boolean finish) {
        final Dialog dialog = new Dialog(mActivity);
        dialog.getWindow().setBackgroundDrawable(new ColorDrawable(android.graphics.Color.TRANSPARENT));
        dialog.requestWindowFeature(Window.FEATURE_NO_TITLE);
        dialog.setContentView(R.layout.dilaog_custom);
        TextView msg = (TextView) dialog.findViewById(R.id.msg1);
        msg.setText(message);
        ImageView img_ok = (ImageView) dialog.findViewById(R.id.img_ok);
        img_ok.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                dialog.dismiss();
                if (finish)
                    ((Activity) mActivity).finish();
                    //paste your code what action perform you want

            }
        });
        ImageView img_cancel = (ImageView) dialog.findViewById(R.id.img_cancel);
        img_cancel.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                dialog.dismiss();
            }
        });
        dialog.getWindow().getAttributes().windowAnimations = R.style.DialogAnimation_2;
        dialog.show();
    }
    
