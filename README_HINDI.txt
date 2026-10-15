ASTRA STRIKE — GITHUB APK BUILDER
Developer: Piyush

GitHub se APK banane ke steps:
1. ZIP ko extract mat karo agar GitHub par upload karne ke liye folder ke andar ke files chahiye hon. ZIP download karke phone ke file manager me extract karo.
2. GitHub.com par login karo aur New repository banao: Astra-Strike (Public ya Private dono chalenge).
3. Repository ke andar Add file > Upload files kholo.
4. Extract kiye hue folder ke ANDAR ke sabhi files/folders upload karo. .github folder bhi upload hona chahiye. Phone me hidden files na dikh rahe hon to GitHub website par workflow file manually create karna pad sakta hai.
5. Commit changes karo.
6. Repository me Actions tab kholo. 'Build Astra Strike APK' workflow chuno. 'Run workflow' dabao.
7. Build green/success ho jaaye to us run ko kholo, neeche Artifacts me 'Astra-Strike-APK' download karo.
8. ZIP artifact ko extract karo; app-debug.apk install karo.

IMPORTANT:
- Game HTML single local file hai: app/src/main/assets/index.html.
- Game internet ke bina chalne ke liye local asset ke roop me pack hota hai. Internet status badge online/offline dikhata hai; is version me multiplayer, online leaderboard, ya server-based online game features nahi hain kyunki unke liye backend/server chahiye.
- APK abhi build nahi hui; GitHub Actions par build chalane ke baad milegi.


MULTIPLAYER NOTE:
Game mein Multiplayer/Friends Hub ka preview section hai. Player UID aur local friend list is device par save hoti hai. Real-time online friend search, friend requests, rooms aur playing together ke liye backend/realtime server connect karna abhi baaki hai; yeh ZIP un features ko real online multiplayer mein magically enable nahi karti.


UPDATE: LANDSCAPE / 16:9
APK अब landscape (आड़ा) orientation में खुलने के लिए सेट है। गेम canvas स्क्रीन के landscape आकार के अनुसार resize होता है।

IMPORTANT — REAL ONLINE MULTIPLAYER
इस ZIP में Multiplayer/Friends Hub अभी केवल local UID/friend list UI है। यह दूसरे फोन पर खिलाड़ियों को खोजने, friend requests भेजने, room बनाकर साथ खेलने या live game state sync करने वाला पूर्ण online multiplayer नहीं है। उसके लिए Firebase/Supabase जैसे backend की project configuration, database security rules और game-state synchronization code जरूरी हैं। बिना आपके backend project/config के इसे सचमुच cross-device multiplayer बताना सही नहीं होगा।


================ FIREBASE ONLINE MULTIPLAYER SETUP ================
ZIP में अब Firebase Authentication + Realtime Database integration का आधार है: online player profile, name/UID search, friend requests/accept, 2–4 player room create/join और ready lobby. यह config लगाए बिना online नहीं चलेगा.

1) https://console.firebase.google.com खोलकर नया project बनाएं.
2) Authentication > Sign-in method में Anonymous sign-in ENABLE करें.
3) Realtime Database बनाएं; region चुनें.
4) Project settings > General > Your apps > Web app में app बनाएं और firebaseConfig की values कॉपी करें.
5) GitHub repository में app/src/main/assets/firebase-config.js खोलें और PASTE_API_KEY_HERE, YOUR_PROJECT_ID, PASTE_APP_ID_HERE को अपनी वास्तविक values से बदलें. databaseURL Firebase Console में दिख रहे exact URL से भरें.
6) Firebase Realtime Database > Rules में database.rules.json की rules paste करके Publish करें.
7) GitHub पर commit करें; Actions > Build Astra Strike APK > Run workflow. नया artifact डाउनलोड करके APK install करें.

IMPORTANT / ईमानदार स्थिति:
- Firebase credentials/config और database rules लगाए बिना कोई ऑनलाइन सर्वर स्वतः नहीं जुड़ सकता; ये आपके Firebase project से ही मिलते हैं.
- यह integration ऑनलाइन खिलाड़ी प्रोफाइल, UID/name खोज, friend requests और 2–4 खिलाड़ी room/lobby को जोड़ता है.
- मौजूदा Astra Strike shooter का core gameplay अभी एकल खिलाड़ी इंजन है. Room members/ready status real-time sync होते हैं, लेकिन एक ही लड़ाई में 2–4 जहाज़, bullets, enemies और scores का synchronized gameplay अभी लागू नहीं है; उसके लिए game engine में authoritative real-time state synchronization अलग से बनानी होगी. इसे पूर्ण live co-op match न समझें.
- Database rules शुरुआती demo rules हैं; public release से पहले server-side validation/Cloud Functions से friend-request और room writes को और सुरक्षित करना चाहिए. API key app config में होना सामान्य है; Firebase service-account/private key कभी APK में न डालें.
