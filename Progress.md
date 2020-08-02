# As of August 1, 2020 3:00 AM

**Fully Completed**

- Main
- Note
- Alarm
- Notification
- Record
- completed all SharedPreferences variables (readnig_plan and reading_day)
- showed full content of each item of ListView
- finished adding some brief messages for each reading plan. 
- finished making textview clickable in Alarm for eaiser selection of checkmarks
- finished changing font size
- added the app icon (shown in the screen) 
- modified squished icon size when font is large
- finished all instruction with fragments
- refreshed Bible fragment
- completed setting - allow textview clickable for easier selection

**Need Help**

- I successfully retrieved data from Firebase, but I cannot show the data using listview nicely (I separated each string with comma, but that limits users to use the comma in their notes).

# Tips I learned

## How to Refresh Fragmnet

Because I spent hours to figure this out, I would like to show some detailed steps to use for later.

[Refreshing a Fragment - Android Geek](https://stackoverflow.com/questions/44622311/how-can-i-call-onactivityresult-inside-fragment-and-how-it-work)

- Step 1. Add the following code in the parent activity java file
```
public void onActivityResult(int requestCode, int resultCode, Intent intent) {
    super.onActivityResult(requestCode, resultCode, intent);
    Fragment fragment = (Fragment) getSupportFragmentManager().findFragmentByTag("FragmentNotes");
    if (fragment != null) {
        fragment.onActivityResult(requestCode, resultCode, intent);
    }
}
```
- Step 2. Add the following code in the child fragment java file
```
@Override
public void onActivityResult(int requestCode, int resultCode, Intent data)
{
    if ((requestCode == 10001) && (resultCode == Activity.RESULT_OK)) {
      // recreate your fragment here
      Fragment frg = null;
      FragmentTransaction ft = getParentFragmentManager().beginTransaction();
      if (Build.VERSION.SDK_INT >= 26) {
          ft.setReorderingAllowed(false);
      }
      ft.detach(this).attach(this).commit();
    }
}
```
- Step 3. Start `startActivityForResult` (not just `startActivity`) from the child fragment to a new activity
```
startActivityForResult(editPrivateData, 10001);
```
- Step 4. Add `setResult` in that new activity
```
setResult(Activity.RESULT_OK);
```

## How to Remotely Upload Android Studio Files in Windows
*Note: Remeber to remove any git connection in Android Studio to use this.*

- Step 1. Open the PowerShell 
- Step 2. Create a folder for Git stuffs
- Step 3. Inside of the folder, type the following code

1. `git init`
2. `git remote add origin http://github.com/gloriakim-cs-projects......`
3. `git pull origin master`
4. Modify the folder as needed (ex) add a new folder
5. `git add .`
6. `git commit -m "Initial commit"`
7. `git push origin master`