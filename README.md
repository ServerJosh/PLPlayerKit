# PLPlayerKit

PLPlayerKit for iOS is an audio and video player SDK, can be highly customized and secondary development, featuring support RTMP and HLS live streaming.

Features

- [X] RTMP Live Streaming
- [X] HLS Play
- [X] highly customizable,
- [X] audio background play
- [X] No ffmpeg dependence

## abstract

- [Quick Start] (# 1 - Quick Start)
- [Configuration Engineering] (# Configure Engineering)
- [Sample code] (# sample code)
- [Version 2.0] (# on version 2.0)
- [Version history] (# version history)

## Quick Start

### Configuration Engineering

- Configure your Podfile file, add the following configuration information

`` `
pod 'PLPlayerKit'
`` `

- Installation CocoaPods dependent

`` `
pod update
`` `
or
`` `
pod install
`` `

-! Done to run your project workspace

### Sample Code

Add where needed

`` `Objective-C
#import <PLPlayerKit / PLPlayer.h>
`` `

initialization

`` `Objective-C
// Initialize Player
PLPlayer * player = [PLPlayer playerWithURL: self.url];

// Set proxy (optional)
player.delegate = self;
`` `

Start / Pause operation

`` `Objective-C
// Prepare Players
__weak typeof (self) wself = self;
[Self.player prepareToPlayWithCompletion: ^ (NSError * error) {
    if (! error) {
        __strong typeof (wself) strongSelf = wself;
        UIView * playerView = strongSelf.player.playerView;
        [StrongSelf.view addSubview: playerView];
    }
}];
   
// Play
[Self.player play];

// time out
[Self.player pause];

// stop
[Self.player stop];
`` `

Players get state

`` `
// Achieve <PLPlayerDelegate> to control the flow state change
- (Void) player: (nonnull PLPlayer *) player statusDidChange: (PLPlayerStatus) state {
// This will return a variety of state of the stream, you can do UI customization and various other business operations according to the state
// In addition to Error state, other states will this method callback
}

- (Void) player: (nonnull PLPlayer *) player stoppedWithError: (nullable NSError *) error {
// When an error occurs, the callback method
}
`` `

Special Note ## audio parts

Because iOS audio resources are designed as a single example of resources, so any change in the player if you do, the outside are likely to be affected, and bring a variety of problems can not be estimated.

In response to this situation, the way PLPlayerKit take is to check whether you can play and take it into the background, while in-house without any settings. In particular by extending the `AVAudioSession` to do, and provides two methods, as follows:

`` `
/ *!
 *description AVAudioSession check the current configuration is the category that can play audio. When the AVAudioSessionCategoryAmbient,
 * AVAudioSessionCategorySoloAmbient, AVAudioSessionCategoryPlayback, AVAudioSessionCategoryPlayAndRecord
 * One when YES, otherwise NO.
 * /
+ (BOOL) isPlayable;

/ *!
 *description Check the current configuration AVAudioSession the category whether background play when the AVAudioSessionCategoryPlayback,
 * AVAudioSessionCategoryPlayAndRecord one when YES, otherwise NO.
 * /
+ (BOOL) canPlayInBackground;
`` `

Resolution can check whether you can play and whether the current category is set background play.

## Known issues

- When the time stamp confusion, player of the current process to be optimized, may be due to a timestamp cause audio Caton phenomenon. This problem can trigger behavior:
    - Push the end plug flow stream after the start, switch to push flow quality
    - Android SDK plug flow before and after the switch to the camera

## Version History

- 2.0.4 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-2.0.4.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-2.0.4.md))
    - Solve possible problems black screen when playing RTMP
- 2.0.3 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-2.0.3.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-2.0.3.md))
    - Solve RTMP play no sound
    - Solve RTMP surge final result in memory can not be played App crash
    - Unable to resolve RTMP only sound playback screen
    - When playing RTMP resolve issues related crash
- 2.0.2 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-2.0.2.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-2.0.2.md))
    - Add RTMP Cache Mechanism
    - Add Data timeout property
    - Fixed memory leak RTMP Play
    - Fixed error problem playing audio RTMP
    - Fix RTMP play the main thread stuck problem
    - Optimized architecture, reduce memory and cpu usage
- 2.0.1 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-2.0.1.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-2.0.1.md))
    - Fixed problem setting is invalid `contentMode`
    - No error is thrown when a problem can not play or play rtmp repair timeout
    - Repair triggered rtmp playing cpu failed surge problem
    - Fixed crash issues may trigger stop
    - Update demo ensure normal running under iOS 9.1
- 2.0.0 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-2.0.0.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-2.0.0.md))
    - Add a new `PLPlayer`, abandoned` PLVideoPlayerController` and `PLAudioPlayerController`
    - When playing RTMP streaming audio and video, into the background sound continues to play, do not disconnect, return the foreground chase frame shows the latest video frame
    - For RTMP live completely optimized seconds on the first screen, minimize cache
    - Completely dependent on ffmpeg, the package volume is reduced again
    - Optimization of resource consumption, reduce memory footprint than the version 1.x more than 50%
- 1.2.22 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.22.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.22.md))
    - Fixed crash caused due to receive a memory warning
    - Fix to stop playing, play state may enter the wrong question
- 1.2.21 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.21.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.21.md))
    - Fix `PLVideoParameterFrameViewContentMode` setting is invalid and` PLVideoParameterDisableDeinterlacing` problem
- 1.2.20 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.20.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.20.md))
    - Fix `seekTo:` the problem of inaccurate
    - Add `PLPlayerStateSeeking` type
- 1.2.19 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.19.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.19.md))
    - Fixed play no return to the status of the problem (for free live stream, hls playback)
    - Fixed no callback stopped at the end of playback problems hls
    - Repair hls playback begins duration of the problem is not 0
- 1.2.18 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.18.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.18.md))
    Fixes prepare state before releasing the audio player will still result in play -
    - Fixed type player status returns incorrect questions
    - Optimization launch resource release
- 1.2.17 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.17.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.17.md))
    - A crash caused when repair timeout
- 1.2.16 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.17.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.16.md))
    - Added support for background playback audio player
    - Add a callback audio player background player mission starts and ends
    - Added setting a long timeout audio and video player
    - Add a method to prepare audio and video player
    - Adding audio and video player completely stopped method
    - Players can not fix the problem released
- 1.2.15 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.15.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.15.md))
    - Fixed problem with AudioPlayer can not play the video stream RTMP streams
- 1.2.14 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.14.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.14.md))
    - Add AudioManager
- 1.2.13 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.13.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.13.md))
    - Adding audio playback controls
    - Updating the parameter field and type to ensure that the generic type can be used in an audio and video player
    - Update type name, increase legibility, reducing ambiguity
- 1.2.12 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.12.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.12.md))
- Change the repo address
- 1.2.11 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.11.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.11.md))
- Add to the application state judge, reduce latency into the background notification failed to suspend play due to crash
- 1.2.10 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.10.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.10.md))
- Adding audio peripherals notification of changes
- Notify add volume when changing
- Add into the phone, and other events cause audio interruption notice
- 1.2.9 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.9.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.9.md))
- Fix crash into the background after
- Updating example in player code, support horizontal and vertical screen rotation operation
- 1.2.8 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.8.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.8.md))
- Add playback progress callback method
- After the repair seekTo flow state is not the right questions
- 1.2.7 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.7.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.7.md))
- Add player state property
- After adding the decoder initialization is complete callback
- Add Player status callback
- After adding the initialization parameter AutoPlay
- 1.2.6 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.6.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.6.md))
- Add an operation to set the playback position
- Added fast forward, rewind operation
- When you add the total play length properties
- Add get property volume
- Add obtain properties of the current playback position
- Add Quiet operation
- 1.2.5 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.5.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.5.md))
- Bug fixes and some of the other library header files conflict
- 1.2.4 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.4.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.4.md))
- Added `` `PLMovieParameterFrameViewContentMode``` parameters
- Bug fixes and some of the other library header files conflict
- Fix the problem Player contentMode can not be changed
- 1.2.3 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.3.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.3.md))
- Fixed initialization occupy the main thread cause problems Caton
- Fixed error callback question invalid
- 1.2.2 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.2.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.2.md))
- Repair lib crash caused by not updating
- 1.2.1 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.1.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.1.md))
- Add a callback failue situations, return NSError objects
- Remove PLVideoPlayerViewController, please use customized PLVideoPlayerController
- 1.2.0 ([Release Notes] (https://github.com/pili-engineering/PLPlayerKit/blob/master/ReleaseNotes/release-notes-1.2.0.md) && [API Diffs] (https: // github.com/pili-engineering/PLPlayerKit/blob/master/APIDiffs/api-diffs-1.2.0.md))
- Lib greatly reduce the size of
- Added customizable playback controls PLVideoPlayerController
- 1.1.2
- Split Flat lib
- Added x86_64 support, ease of debugging used in iPhone 6 Plus simulator
- 1.1.1
- A reference to the library to do some changes
- 1.1.0
- Post CocoaPods version
