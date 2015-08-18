# How to setup SimBox as a Simulator

Windows Instructions(NEW!)

Step 1: Download and install OBS MultiPlatform

    $ https://obsproject.com/index (Project)
    $ https://github.com/jp9000/obs-studio/releases/download/0.11.4/OBS-MP-0.11.4-Installer.exe (Direct Link)

Step 2: Open cantren.github.io(or local copy) in Chrome

Step 3: Create a new Scene

Step 4: Create a new Source(Type: Window Capture)

Step 5: Select the Chrome window running SimBox

Step 6: Right click on the captured area and choose "Filters" from the drop down menu

Step 7: Select "Crop" Width = 728 and Height = 728 

    Note: x/y position will be found by subtracting "728" from your screen resolution $width and $height respectively and         dividing the result by two

Step 8: ???

TODO:How to use FFServer as RTMP server instead of Twitch.tv etc?(firewall problems?)

TODO:What did I gloss over in video settings etc?

Windows Instructions(old)

Step 1: Download and install LIVE555 RTSP Server

    $ http://www.live555.com/mediaServer/

Step 2: Install ffmpeg for windows

Step 3: Install "screen-capture-recorder" http://sourceforge.net/projects/screencapturer/files/Setup%20Screen%20Capturer%20Recorder%20v0.12.8.exe/download

Step 4: ffmpeg -f dshow -i video="screen-capture-recorder" C:\Users\[your username]\Desktop\output.mp4

TODO: Improve the above command to use a windows RTSP server

Linux Instructions

Step 1: Compile FFMPEG (with x11grab)(Alternate instructions can be found here): https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu

    $ sudo apt-get remove ffmpeg x264 libx264-dev
    $ sudo apt-get update
    $ sudo apt-get install build-essential checkinstall git libfaac-dev libjack-jackd2-dev
    $ sudo apt-get install libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libsdl1.2-dev libtheora-dev
    $ sudo apt-get install libva-dev libvdpau-dev libvorbis-dev libx11-dev libxfixes-dev libxvidcore-dev texi2html
    $ sudo apt-get install yasm zlib1g-dev


    $ cd ~/sources
    $ git clone git://git.videolan.org/x264
    $ cd x264
    $ ./configure --enable-static
    $ make
    $ sudo checkinstall --pkgname=x264 --pkgversion="3:$(./version.sh|awk -F'[" ]' '/POINT/{print $4"+git"$5}')" --backup=no --deldoc=yes --fstrans=no --default


    $ cd ~/sources
    $ git clone git://git.videolan.org/ffmpeg
    $ cd ffmpeg
    $ ./configure --enable-gpl --enable-libfaac --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libtheora --enable-libvorbis --enable-libx264 --enable-libxvid --enable-nonfree --enable-postproc --enable-version3 --enable-x11grab
    $ make
    $ sudo checkinstall --pkgname=ffmpeg --pkgversion="5:$(date +%Y%m%d%H%M)-git" --backup=no --deldoc=yes --fstrans=no --default
    $ sudo ln -s /home/user/ffmpeg/ffmpeg /usr/bin/ffmpeg

Step 2: Create/Edit /etc/ffserver.conf

    $ sudo nano /etc/ffserver.conf

Step 3: Copy and paste contents of ffserver.conf from the "cantren.github.io/Install Instructions" to your terminal.

File location: /etc/ffserver.conf:
[contents]

    Port 8090
    BindAddress 0.0.0.0
    MaxHTTPConnections 30
    MaxClients 20
    MaxBandwidth 2000
    CustomLog - 


    <Feed feed1.ffm>
        File /tmp/feed1.ffm
        FileMaxSize 1G 
        ACL allow 127.0.0.1
    </Feed>
    <Feed feed2.ffm>
        File /tmp/feed2.ffm
        FileMaxSize 1G
        ACL allow 127.0.0.1
    </Feed>
    <Feed feed3.ffm>
        File /tmp/feed3.ffm
        FileMaxSize 1G
        ACL allow 127.0.0.1
        ACL allow 192.168.1.4
    </Feed>
    <Stream simboxBig.swf>
        Feed feed3.ffm
        Format swf
        VideoFrameRate 10
        VideoBitRate 256
        VideoQMin 2
        VideoQMax 8
        VideoSize 728x728
        NoAudio
    </Stream>
    <Stream simbox.swf>
    Feed feed2.ffm
        Format swf
        VideoFrameRate 10
        VideoBitRate 256
        VideoQMin 2
        VideoQMax 8
        VideoSize 200x200
        NoAudio
    </Stream>
    <Stream live.flv>
        Format flv
        Feed feed1.ffm
        VideoCodec libx264
        VideoFrameRate 10
        VideoSize 728x728
        VideoBitRate 256
        VideoBufferSize 0
        VideoGopSize 2
        AVOptionVideo tune zerolatency
        AVOptionVideo crf 23
        AVOptionVideo me_range 4
        AVOptionVideo qdiff 1
        AVOptionVideo qmin 2
        AVOptionVideo qmax 8
        AVOptionVideo flags +global_header
        NoAudio
    </Stream>
    <Stream stat.html>
        Format status
        ACL allow localhost
    </Stream>
[/contents]


Step 4: [Ctrl]+[x] keys

Step 5: [y] key

Step 6: [enter] key

Step 7: 

    $ cd ~/ffmpeg
    $ ./ffserver

Step 8: In Another terminal:

    $ cd ~/ffmpeg
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
    cv::VideoWriter outStream("http://localhost:8090/feed2.ffm", CV_FOURCC('F', 'L', 'V', '1'), 10, cv::Size(200, 200), true);

Step 11: Go back to your web browser

Step 12: Go to full screen

Step 13: Refresh the page using the [F5] key

Step 14: Press [spacebar] to start Vunit's "autopilot mode".
