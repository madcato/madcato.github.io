---
layout:     post
title:      "iOS 7 Grabación de Audio"
date:       2014-02-07 12:09:00
author:     "Daniel Vela"
header-img: "img/post-bg-01.jpg"
---

Para grabar sonido con iOS 7 hay que usar la clase **AVAudioRecorder**.

Antes de iniciar la grabación con el método **record** hay que invocar el método **prepareToRecord**. Ambos métodos devuelven un booleano como valor de retorno. Es muy importante comprobar que devuelven **YES**. En caso contrario mostrar un error ya que la grabación no se iniciará.

## Creación y configuración de AVAudioRecorder

El objeto AVAudioRecorder requiere para su inicialización un objeto **NSDictionary** con los siguientes valores:

{% highlight objective-c %}
@{AVFormatIDKey:@(kAudioFormatMPEG4AAC),
  AVSampleRateKey:@44100.0,
  AVNumberOfChannelsKey:@2,
  AVEncoderAudioQualityKey:@(AVAudioQualityMin),
  AVEncoderBitRateKey:@16,
};
{% endhighlight %}

Además de crear este objeto **NSDictionary** es necesario realizar un paso anterior: crear un objeto **AVAudioSesion**.

A partir de iOS 7 se hace imprescindible crear un objeto **AVAudioSession** antes de crear el objeto **AVAudioRecorder**. En caso contrario la grabación no se iniciará.

![Sesión de grabación de audio]({{ site.url }}/assets/tumblr_inline_n0mhtxb2Q31qjhbuu.png)

{% highlight objective-c %}
Ejemplo de código

//
//  ViewController.m
//  NoiseAlertPrototype
//
//  Created by Daniel Vela on 30/01/14.
//  Copyright (c) 2014 veladan. All rights reserved.
//

#import "ViewController.h"

const float min_level = 20.0f;
const float max_level = 160.0f;

@interface ViewController ()

@end

@implementation ViewController

-(AVAudioRecorder*)recorder {
    if (_recorder == nil) {
        NSURL* url = [[[NSFileManager defaultManager] URLsForDirectory:NSDocumentDirectory
                                                             inDomains:NSUserDomainMask]
                      lastObject];
        url = [url URLByAppendingPathComponent:@"record.aac"];
        NSDictionary* settings = @{AVFormatIDKey:@(kAudioFormatMPEG4AAC),
                                   AVSampleRateKey:@44100.0,
                                   AVNumberOfChannelsKey:@2,
                                   AVEncoderAudioQualityKey:@(AVAudioQualityMin),
                                   AVEncoderBitRateKey:@16,

                                   };
        AVAudioSession *audioSession = [AVAudioSession sharedInstance];
        [audioSession setCategory:AVAudioSessionCategoryRecord
                            error:nil];
        NSError* error;
        _recorder = [[AVAudioRecorder alloc] initWithURL:url
                                                    settings:settings
                                                       error:&error];
        if (error) {
            UIAlertView* alert = [[UIAlertView alloc] initWithTitle:@"Error creating audio recorder"
                                                            message:[error description]
                                                           delegate:nil
                                                  cancelButtonTitle:@"cancel"
                                                  otherButtonTitles:nil];
            [alert show];
        }
        _recorder.meteringEnabled = YES;

    }
    return _recorder;
}

- (void)viewDidLoad
{
    [super viewDidLoad];

    [self setStop];
    [self startTakingNoiseSamples];
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

float adjustNoiseLevel(float value) {
    if (value > 0) value = 0;
    value = max_level + value;
    value = value / max_level;
    return value;
}

- (void)setAverageLevelValue:(float)value {
    value = adjustNoiseLevel(value);
    [self.averageLevel setProgress:value];
}

- (void)setPeakLevelValue:(float)value  {
    value = adjustNoiseLevel(value);
    [self.peakLevel setProgress:value];
}

- (void)startTakingNoiseSamples {

    if ([self.recorder isRecording] == YES) {
        [self.recorder updateMeters];
        float averagePower = [self.recorder averagePowerForChannel:0];
        float peakPower = [self.recorder peakPowerForChannel:0];
        [self setAverageLevelValue:averagePower];
        [self setPeakLevelValue:peakPower];
    }

    [self performSelector:@selector(startTakingNoiseSamples)
               withObject:nil
               afterDelay:0.05f];
}

- (void)startRecording {
    [self setStart];
    BOOL prepared = [self.recorder prepareToRecord];
    if (prepared == NO) {
        UIAlertView* alert = [[UIAlertView alloc] initWithTitle:@"Error creating audio recorder"
                                                        message:@"no preparado"
                                                       delegate:nil
                                              cancelButtonTitle:@"cancel"
                                              otherButtonTitles:nil];
        [alert show];

    }
    BOOL started = [self.recorder record];
    if (started == NO) {
        UIAlertView* alert = [[UIAlertView alloc] initWithTitle:@"Error starting recording"
                                                        message:@"no preparado"
                                                       delegate:nil
                                              cancelButtonTitle:@"cancel"
                                              otherButtonTitles:nil];
        [alert show];

    }

}

- (void)stopRecording {
    [self setStop];
    [self.recorder stop];
}

- (void)setStop {
    [self.startStopButton setTitle:@"Start" forState:UIControlStateNormal];
    [self.startStopButton addTarget:self
                          action:@selector(startRecording)
                forControlEvents:UIControlEventTouchUpInside];
}

- (void)setStart {
    [self.startStopButton setTitle:@"Stop" forState:UIControlStateNormal];
    [self.startStopButton addTarget:self
                          action:@selector(stopRecording)
                forControlEvents:UIControlEventTouchUpInside];
}


@end
{% endhighlight %}