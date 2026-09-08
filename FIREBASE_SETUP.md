# Firebase Setup — V S Enterprises Attendance

1. Create a Firebase project and add the Android app with package `com.vsenterprises.attendance`.
2. Download `google-services.json` and put it in `app/`.
3. Enable Authentication → Phone sign-in method.
4. Enable Firestore Database (production mode).
5. Publish the security rules from `firestore.rules`.
6. Add a Google Maps API key in `AndroidManifest.xml` (already added).

## Making someone an Admin (to view the Live Team Map)

By default every employee who logs in gets `isAdmin: false`. To give someone
access to the "Live Team Map" screen:

1. Ask that employee to log in to the app once (so their profile document is created).
2. Go to Firebase Console → Firestore Database → `employees` collection.
3. Find their document (it's named with their Firebase user ID).
4. Edit the field `isAdmin` and change its value from `false` to `true` (boolean).
5. They will now see the "Live Team Map" button next time they open the Dashboard.

## Data structure

- `employees/{uid}`: name, employeeId, mobile, isAdmin, sharing, liveLat, liveLng, liveUpdatedAt
- `attendance/{autoId}`: uid, employeeName, type (checkin/checkout), timestamp, dutyDurationHours

## Notes

- Free plan (Spark) limits phone-auth SMS to 10/day. Add a billing account
  (Blaze plan, still has a generous free tier) to raise this limit once you
  have more employees testing.
- The Maps API key currently has no restrictions. For production, restrict it
  to Android apps with package `com.vsenterprises.attendance` and your app's
  SHA-1 fingerprint (Firebase Console → Project settings → Your apps).
