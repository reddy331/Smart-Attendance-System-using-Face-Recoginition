
# Face Recognition Based Attendance System

This project uses Python's `face_recognition` and `OpenCV` libraries to build a face recognition system for identifying students and marking attendance. The face encodings of students are stored and used to identify individuals from live camera feeds or images.

## Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [File Structure](#file-structure)
- [Firebase Integration](#firebase-integration)
- [License](#license)

## Features
- Face encoding and recognition using `face_recognition`.
- Store student IDs along with their face encodings.
- Save the encoded data to a file for later use.
- Firebase integration for storing images and future extensions such as database and cloud storage.
  
## Technologies Used
- Python
- OpenCV
- face_recognition
- Firebase (for storage and future database integration)
- Pickle (for serializing encodings)

## Setup and Installation

1. **Clone the repository:**
   \`\`\`bash
   git clone https://github.com/yourusername/face-recognition-attendance.git
   cd face-recognition-attendance
   \`\`\`

2. **Install dependencies:**
   \`\`\`bash
   pip install opencv-python
   pip install face-recognition
   pip install firebase-admin
   \`\`\`

3. **Set up Firebase:**
   - Go to the [Firebase Console](https://console.firebase.google.com/), create a new project, and enable Firebase Realtime Database and Cloud Storage.
   - Download your Firebase Admin SDK service account key (`serviceAccountKey.json`).
   - Place the `serviceAccountKey.json` file in the root directory of the project.

4. **Edit Firebase Credentials:**
   - Uncomment the following lines in the main script and add your Firebase project credentials:
   \`\`\`python
   cred = credentials.Certificate("serviceAccountKey.json")
   firebase_admin.initialize_app(cred, {
      'databaseURL': "YOUR_DATABASE_URL",
      'storageBucket': "YOUR_STORAGE_BUCKET_URL"
   })
   \`\`\`

5. **Prepare the Images:**
   - Create a folder named `Images` in the project directory.
   - Add images of students into the `Images` folder. The image filenames should match the student IDs (e.g., `12345.jpg` for a student with ID `12345`).

6. **Run the Script:**
   - To encode the images and save them in a serialized file:
     \`\`\`bash
     python encode_faces.py
     \`\`\`

## Usage

1. **Face Encoding:**
   - The script reads all the student images from the `Images` folder, encodes their faces, and saves the encodings in a file named `EncodeFile.p` using `pickle`.

2. **Firebase Integration:**
   - The commented-out Firebase code (currently optional) allows the project to upload images to Firebase Storage. In future versions, this can be extended for live attendance tracking and storing attendance data in Firebase Realtime Database.

3. **Image Processing:**
   - The `cv2.imread()` function reads images, which are then converted to RGB using OpenCV and encoded using `face_recognition.face_encodings()`. These encodings are stored along with the respective student IDs.

## File Structure

\`\`\`
face-recognition-attendance/
│
├── Images/                   # Folder containing student images
│   ├── student1.jpg
│   └── student2.jpg
│
├── encode_faces.py            # Script to encode faces and save them
├── serviceAccountKey.json     # Firebase service account credentials (not included for security reasons)
├── EncodeFile.p               # Saved pickle file with face encodings and student IDs
├── README.md                  # Project documentation
\`\`\`

## Firebase Integration
To enable Firebase in the system:

1. **Storage**: The script is set up to upload student images to Firebase Cloud Storage (commented out by default).
2. **Realtime Database**: Future versions can be extended to record attendance data directly in Firebase's Realtime Database.

Ensure you have enabled these services in Firebase and updated the project with your credentials.

## License
This project is licensed under the MIT License. See the `LICENSE` file for more information.
