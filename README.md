# Svelte Scroll Video

A component to play a video by scrolling the page

## Installation

```shell
$ npm install @macfja/svelte-scroll-video
# or
$ yarn add @macfja/svelte-scroll-video
# or
$ pnpm add @macfja/svelte-scroll-video
```

## Usage

```html
<script>
  import ScrollVideo from "@macfja/svelte-scroll-video";
</script>

<p>...</p>
<ScrollVideo src="https://example.com/my-video.webm" />
<p>...</p>
```

[Example on REPL](https://svelte.dev/repl/f90faa36aca24862aeca378fc3d7e211)

## Configurations

| Option               | Type         | Default       | Description                                                                                                                 |
| -------------------- | ------------ | ------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `pixelPerSec`        | Prop         | `1000`        | Number of pixel to scroll for 1 sec of video                                                                                |
| `on:playing`         | Event        | _N/A_         | This event is dispatched every times the playing status changes (`event.detail` contain `true` if the video is progressing) |
| `on:position`        | Event        | _N/A_         | This event is dispatched every times the playback is updated (`event.detail` contain the number of seconds elapsed)         |
| `--video-background` | CSS Property | `transparent` | The color behind the video                                                                                                  |
| `--video-height`     | CSS Property | `100vh`       | The height of the video                                                                                                     |
| _any value_          | Prop         | _empty_       | All attribute you want to pass to the `<video>` element                                                                     |
| _any value_          | Slot         | _empty_       | Any data that you want to be a child of the `<video>` element                                                               |

```html
<ScrollVideo
    pixelPerSec="250"
    on:playing={e => console.log('The video is ' + (e.detail?'playing':'in pause')}
    on:position={e => console.log('The video is at its '+(e.detail)+' seconds')}
    --video-background="black"
    --video-height="90vh"
    src="https://example.com/my-video.webm"
>
    <track src="https://example.com/captions.srt" kind="captions" />
</ScrollVideo>
```

## Examples

See [Examples.md](./docs/Examples.md)

## Contributing

Contributions are welcome. Please open up an issue or create PR if you would like to help out.

Read more in the [Contributing file](CONTRIBUTING.md)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
