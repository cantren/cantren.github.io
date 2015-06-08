Step 1: Compile FFMPEG (with x11grab)

Instructions here: https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu

Step 2: Create/Edit /etc/ffserver.conf

$ sudo nano /etc/ffserver.conf

Step 3: Copy and paste contents of ffserver.conf from the "cantren.github.io/Install Instructions" to your terminal.

Step 4: [Ctrl]+[x] keys

Step 5: [y] key

Step 6: [enter] key

Step 7: 

$ cd ~/bin

$ ./ffserver

Step 8: In Another terminal:

$ cd ~/bin

$ ./ffmpeg -f x11grab -r 10 -s 728x728 -i :0.0+319,19 -vcodec libx264 -tune zerolatency -pix_fmt yuv420p -s 728x728 -threads 0 http://localhost:8090/feed1.ffm

Step 9: Open "cantren.gihub.io" in your web browser

Step 10: Run OpenCV program "Vunit" in autopilot mode

OR

Step 10: Use the following OpenCV VideoCapture settings:

  cv::VideoCapture cap;

  cap.open("http://localhost:8090/live.flv"); // open the default camera

  cap.set(CV_CAP_PROP_FOURCC, CV_FOURCC('F', 'L', 'V', '1'));

AND

  cv::resize(frame, frame, cv::Size(200, 200));

  cv::VideoWriter outStream("http://localhost:8090/feed2.ffm", CV_FOURCC('F', 'L', 'V', '1'), 10, cv::Size(200, 
200), true);

Step 11: Go back to your web browser

Step 12: Go to full screen

Step 13: Refresh the page using the [F5] key

Step 14: Press [spacebar] to start Vunit's "autopilot mode".
