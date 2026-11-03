# Application Exercise: Inheritance with Media

Consider this class diagram:

![MediaStream Inheritance Diagram](MediaStreamInheritance.png)

Which of the following is the best implementation of this design?

- Option A

```csharp
class MediaStream
{
    protected string _title;
    protected int _durationSeconds;

    public MediaStream(string title, int durationSeconds)
    {
        _title = title;
        _durationSeconds = durationSeconds;
    }

    public void Play()
    {
        Console.WriteLine($"Playing {_title}.");
    }

    public void Pause()
    {
        Console.WriteLine($"Pausing {_title}.");
    }
}

class AudioStream : MediaStream
{
    private int _sampleRateHz;
    private int _channelCount;

    public AudioStream(string title, int durationSeconds, int sampleRateHz, int channelCount)
        : base(title, durationSeconds)
    {
        _sampleRateHz = sampleRateHz;
        _channelCount = channelCount;
    }

    public void SetEqualizerPreset(string preset)
    {
        Console.WriteLine($"Setting equalizer to {preset}.");
    }
}

class VideoStream : AudioStream
{
    private string _resolution;
    private int _frameRate;

    public VideoStream(
        string title,
        int durationSeconds,
        int sampleRateHz,
        int channelCount,
        string resolution,
        int frameRate)
        : base(title, durationSeconds, sampleRateHz, channelCount)
    {
        _resolution = resolution;
        _frameRate = frameRate;
    }

    public void ChangeResolution(string resolution)
    {
        _resolution = resolution;
        Console.WriteLine($"Changing resolution to {_resolution}.");
    }
}
```

- Option B

```csharp
class MediaStream
{
    protected string _title;
    protected int _durationSeconds;
    protected int _sampleRateHz;
    protected int _channelCount;
    protected string _resolution;
    protected int _frameRate;

    public void Play()
    {
        Console.WriteLine($"Playing {_title}.");
    }

    public void Pause()
    {
        Console.WriteLine($"Pausing {_title}.");
    }

    public void SetEqualizerPreset(string preset)
    {
        Console.WriteLine($"Setting equalizer to {preset}.");
    }

    public void ChangeResolution(string resolution)
    {
        _resolution = resolution;
        Console.WriteLine($"Changing resolution to {_resolution}.");
    }
}

class AudioStream : MediaStream
{
    public AudioStream(string title, int durationSeconds, int sampleRateHz, int channelCount)
    {
        _title = title;
        _durationSeconds = durationSeconds;
        _sampleRateHz = sampleRateHz;
        _channelCount = channelCount;
    }
}

class VideoStream : MediaStream
{
    public VideoStream(string title, int durationSeconds, string resolution, int frameRate)
    {
        _title = title;
        _durationSeconds = durationSeconds;
        _resolution = resolution;
        _frameRate = frameRate;
    }
}
```

- Option C

```csharp
class MediaStream
{
    protected string _title;
    protected int _durationSeconds;

    public MediaStream(string title, int durationSeconds)
    {
        _title = title;
        _durationSeconds = durationSeconds;
    }

    public void Play()
    {
        Console.WriteLine($"Playing {_title}.");
    }

    public void Pause()
    {
        Console.WriteLine($"Pausing {_title}.");
    }
}

class AudioStream : MediaStream
{
    protected new string _title;
    protected new int _durationSeconds;
    private int _sampleRateHz;
    private int _channelCount;

    public AudioStream(string title, int durationSeconds, int sampleRateHz, int channelCount)
        : base(title, durationSeconds)
    {
        _title = title;
        _durationSeconds = durationSeconds;
        _sampleRateHz = sampleRateHz;
        _channelCount = channelCount;
    }

    public void SetEqualizerPreset(string preset)
    {
        Console.WriteLine($"Setting equalizer to {preset}.");
    }
}

class VideoStream : MediaStream
{
    protected new string _title;
    protected new int _durationSeconds;
    private string _resolution;
    private int _frameRate;

    public VideoStream(string title, int durationSeconds, string resolution, int frameRate)
        : base(title, durationSeconds)
    {
        _title = title;
        _durationSeconds = durationSeconds;
        _resolution = resolution;
        _frameRate = frameRate;
    }

    public void ChangeResolution(string resolution)
    {
        _resolution = resolution;
        Console.WriteLine($"Changing resolution to {_resolution}.");
    }
}
```

- Option D

```csharp
class MediaStream
{
    protected string _title;
    protected int _durationSeconds;

    public MediaStream(string title, int durationSeconds)
    {
        _title = title;
        _durationSeconds = durationSeconds;
    }

    public void Play()
    {
        Console.WriteLine($"Playing {_title}.");
    }

    public void Pause()
    {
        Console.WriteLine($"Pausing {_title}.");
    }
}

class AudioStream : MediaStream
{
    private int _sampleRateHz;
    private int _channelCount;

    public AudioStream(string title, int durationSeconds, int sampleRateHz, int channelCount)
        : base(title, durationSeconds)
    {
        _sampleRateHz = sampleRateHz;
        _channelCount = channelCount;
    }

    public void SetEqualizerPreset(string preset)
    {
        Console.WriteLine($"Setting equalizer to {preset}.");
    }
}

class VideoStream : MediaStream
{
    private string _resolution;
    private int _frameRate;

    public VideoStream(string title, int durationSeconds, string resolution, int frameRate)
        : base(title, durationSeconds)
    {
        _resolution = resolution;
        _frameRate = frameRate;
    }

    public void ChangeResolution(string resolution)
    {
        _resolution = resolution;
        Console.WriteLine($"Changing resolution to {_resolution}.");
    }
}
```