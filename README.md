# AOSP Builder
Build aosp project in docker with Ubuntu 20.04 via ci environments (by [Apon77](https://github.com/Apon77))

Thanks to Almighty Who has given mental strength, knowledge, and patience.

Thanks to [Cirrus CI](https://cirrus-ci.com/) for their awesome service!

I tried to explain every step by comments! Try to read those thoroughly!

[ You can use your own creativity for this whole process, what I did is used the normal process, collected the cache, redownloaded, and re reused it, and for overcoming the time limit first build was done with a timeout from our side to get ccache uploaded. You can do these processes manually too! But I like ci! Let's a ci be ci, hehe. ]

## Steps:

1. Fork this repo
2. Go to https://github.com/marketplace/cirrus-ci
3. Pricing and setup > Public Repositories > Install it for free
4. On the next page click Complete order and begin installation
5. On the next page select All repositories or only selected repository (select aosp-builder) > Install
6. On the next page give password and Confirm the password
7. Setup is done for cirrus ci in your account! You can close the tab now!
8. Install rclone in any pc and setup any cloud drive, where to store cccahe. Setup rclone and collect the content of ~/.config/rclone/rclone.conf and paste that inside cirrus ci repository secret, explained in .cirrus.yml file. You can take the help of [rclone website](https://rclone.org). It's recommended to use your own client id and secret, but you can use rclone default config if you can sacrifice some speed (_60MBPS vs 7MBPS upload speed_)! You can use a normal google account rather than team drive too! ccache will be fit inside the 15GB drive limit hopefully! 
9. Setup google drive index with the help of any of these two or any gdrive index you want.

* https://github.com/maple3142/GDIndex \
or,
* https://github.com/Achrou/goindex-theme-acrou

so that it can be accessed URL like this https://roms.apon77.workers.dev with a persistence link! Because ccache needs to be downloaded every time you build! You can do your creativity to download and upload ccache. That's your choice! I use google drive for the speed and not to change the ccache url always! Rclone is a better choice from my perspective.

**I prefer using rclone own id config for google drive team drive with google drive index**
 
10.  All other steps can be found inside every script! Please read those carefully.
11.  After setting up all other scripts according to your needs, then just do any commit in this repo, and the build will be triggered! \
Whenever you need a build you can just commit in this repo. By the way, check the cpu count when you start build, it's recommended to use 8cpu and less for the flexibility (in .cirrus.yml file). The highest cpu limit is 8 for free accounts.
12. First commit build should be stopped immediately with 1cpu, and setup your rclone_config encrypted variable in cirrus ci repo, instructed in .cirrus.yml file. Please use your own rclone_config variable in .cirrus.yml. Otherwise, you may not be able to complete the build. \
Your build log must not be yellow marked as "Failed to decrypt some environment variables: NOT_FOUND:".
13. Later 2 builds should be with 8cpu to collect and upload ccache, also instructed within scripts. This collecting cccahe step (both upload and download) is very important. Also using rclone(own config) is mendatory.  It's highly recommended to use google drive in all kind of cloud transfer for speed. Also don't sync unnecessary repos in sync script. Without these things probably you won't be able to succeed to get a build.
14. I apologize that, this repo came with some previous ccache. I got that when I was testing. \
So, for your convenience, https://github.com/Apon77Lab/aosp-builder did fork this repo and did essential commits and got a successful build, which is almost identical to your situation and has no previous ccache. It's highly recommended that you should observe carefully his commits to know what you actually need to do in scripts. For little support, you can contact me here! https://t.me/Apon77Mido

**Humble request to all not to abuse this system. Happy building!!!**
