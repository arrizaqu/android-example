#Android Example
1. Android Console with Log Util
2. Toast
3. Event Listener
4. Alert Dialog
5. Back Button twice To exit
6. Activity to Another Activity with Intent
7. Data Populate with List View
8. Passing Data with Bundle
9. SharedPrefference


#Andorid Console Log Util
	- code :
        Log.d("myconsole", "works!!");

#Toast 
	- code : 
		Context context = getApplicationContext();
        int myLong = Toast.LENGTH_LONG;
        Toast myToast = Toast.makeText(context, "hello world ", myLong);
        myToast.setGravity(Gravity.TOP | Gravity.CENTER, 0, 0);
        myToast.show();

#Event Listener 
	- code :
		 button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Log.d("myconsole", "click me");
            }
        });

#Alert Dialog
	- code : 
		public Dialog onCreateDialog() {
        // Use the Builder class for convenient dialog construction
			AlertDialog.Builder builder = new AlertDialog.Builder(this);
			builder.setMessage("Are  your sure ?")
					.setPositiveButton("OK", new DialogInterface.OnClickListener() {
						public void onClick(DialogInterface dialog, int id) {
							// FIRE ZE MISSILES!
							Log.d("myconsole", "OKE");
						}
					})
					.setNegativeButton("CANCEL", new DialogInterface.OnClickListener() {
						public void onClick(DialogInterface dialog, int id) {
							// User cancelled the dialog
							Log.d("myconsole", "CANCEL");
						}
					});
			// Create the AlertDialog object and return it
			return builder.create();
		}
		
#Back Button twice To exit
	- code : 
		boolean doubleBackToExitPressedOnce = false;

		@Override
		public void onBackPressed() {
			if (doubleBackToExitPressedOnce) {
				super.onBackPressed();
				return;
			}

			this.doubleBackToExitPressedOnce = true;
			Toast.makeText(this, "Please click BACK again to exit", Toast.LENGTH_SHORT).show();

			new Handler().postDelayed(new Runnable() {

				@Override
				public void run() {
					doubleBackToExitPressedOnce=false;                       
				}
			}, 2000);
		}

#Activity to Another Activity with Intent
	- code : 
		public final static String EXTRA_MESSAGE = "com.example.myfirstapp.MESSAGE";
		public void sendMessage(View view) {
			Intent intent = new Intent(this, DisplayMessageActivity.class);
			EditText editText = (EditText) findViewById(R.id.edit_message);
			String message = editText.getText().toString();
			intent.putExtra(EXTRA_MESSAGE, message);
			startActivity(intent);
		}

#Data Populate with List View
	- code: 
		- single view
			ListView listView = (ListView) findViewById(R.id.lvItems);
			String cities[] = new String[]{"jakarta", "bandung", "surabaya", "seputih banyak"};
			ArrayAdapter dataAdapter = new ArrayAdapter(this, android.R.layout.simple_list_item_1, cities);
			listView.setAdapter(dataAdapter);
			
		- multiple view
			- User Entity :
				class User {
					public String name;
					public String hometown;

					public User(String name, String hometown) {
						this.name = name;
						this.hometown = hometown;
					}
				}
			
			- View XML : 
				<?xml version="1.0" encoding="utf-8"?>
				<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
					android:orientation="vertical" android:layout_width="match_parent"
					android:layout_height="match_parent" >
					<TextView
						android:id="@+id/tvName"
						android:layout_width="wrap_content"
						android:layout_height="wrap_content"
						android:textSize="20dp"
						android:layout_marginRight="20dp"
						android:textColor="#000"
						android:text="Name" />
					<TextView
						android:id="@+id/tvHome"
						android:layout_width="wrap_content"
						android:textSize="30dp"
						android:textColor="#000"
						android:layout_height="wrap_content"
						android:text="HomeTown" />
				</LinearLayout>
				
			- Java Code : 
				- Main 
					List<User> listUser = new ArrayList();
					listUser.add(new User("masyda arrizaqu", "seputih banyak"));
					listUser.add(new User("wildan", "bogor"));
					listUser.add(new User("ujang", "Jakarta"));
					ListView listView22 = (ListView) findViewById(R.id.lvItems2);
					UsersAdapter usersAdapter = new UsersAdapter(getApplicationContext(), listUser);
					listView2.setAdapter(usersAdapter);
					
				- Java and Custome Adapter
					class UsersAdapter extends ArrayAdapter<User> {
						// View lookup cache
						private static class ViewHolder {
							TextView name;
							TextView home;
						}

						public UsersAdapter(Context context, List<User> users) {
							super(context, R.layout.item_user, users);
						}

						@Override
						public View getView(int position, View convertView, ViewGroup parent) {
							// Get the data item for this position
							User user = getItem(position);
							// Check if an existing view is being reused, otherwise inflate the view
							ViewHolder viewHolder; // view lookup cache stored in tag
							if (convertView == null) {
								// If there's no view to re-use, inflate a brand new view for row
								viewHolder = new ViewHolder();
								LayoutInflater inflater = LayoutInflater.from(getContext());
								convertView = inflater.inflate(R.layout.item_user, parent, false);
								viewHolder.name = (TextView) convertView.findViewById(R.id.tvName);
								viewHolder.home = (TextView) convertView.findViewById(R.id.tvHome);
								// Cache the viewHolder object inside the fresh view
								convertView.setTag(viewHolder);
							} else {
								// View is being recycled, retrieve the viewHolder object from tag
								viewHolder = (ViewHolder) convertView.getTag();
							}
							// Populate the data into the template view using the data object
							viewHolder.name.setText(user.name);
							viewHolder.home.setText(user.hometown);
							// Return the completed view to render on screen
							return convertView;
						}
					}

#Passing Data with Bundle
	- code : 
		- Write and Create the Bundle
			//Create the bundle
			Bundle bundle = new Bundle();
			//Add your data from getFactualResults method to bundle
			bundle.putString("VENUE_NAME", venueName);
			//Add the bundle to the intent
			i.putExtras(bundle);
			startActivity(i);

		- Read and Get Data the Bundle
			Bundle bundle = getIntent().getExtras();
			//Extract the data…
			String venName = bundle.getString("VENUE_NAME");        

#SharedPrefference
	- code : 
		- Write to Shared Preferences: 
		
			SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
			SharedPreferences.Editor editor = sharedPref.edit();
			editor.putInt(getString(R.string.saved_high_score), newHighScore);
			editor.commit();
			
		- Read from Shared Preferences: 
		
			SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
			int defaultValue = getResources().getInteger(R.string.saved_high_score_default);
			long highScore = sharedPref.getInt(getString(R.string.saved_high_score), defaultValue);
			
#Reference 
	1. https://developer.android.com/guide/webapps/debugging.html
	2. https://developer.android.com/guide/topics/ui/notifiers/toasts.html
	3. https://developer.android.com/guide/topics/ui/dialogs.html
	4. http://stackoverflow.com/questions/8430805/clicking-the-back-button-twice-to-exit-an-activity
	5. https://developer.android.com/training/basics/firstapp/starting-activity.html
	6. http://stackoverflow.com/questions/15445182/passing-data-from-one-activity-to-another-using-bundle-not-displaying-in-secon