# winutil-exe

Nightly automated build of [ChrisTitusTech/winutil](https://github.com/ChrisTitusTech/winutil)
as a Windows executable, published on the [Releases](../../releases) page.

> **This is an unofficial repackaging for personal use** — not the original
> project, and not affiliated with CT Tech Group LLC or Chris Titus Tech.
> See [NOTICE](NOTICE). For the real project, issues, and support, use the
> upstream repository.

## How it works

Every night at 03:00 UTC, [the workflow](.github/workflows/build.yml):

1. **check** (ubuntu, seconds): compares upstream's latest release tag with our
   latest release. No new tag → done, nothing built.
2. **build** (windows, only when the tag is new): downloads the unmodified
   `winutil.ps1` from the upstream release, wraps it into `winutil.exe` with
   [ps2exe](https://github.com/MScholtes/PS2EXE), verifies the output, and
   publishes it as a release under the same tag.

The script itself is never modified — the exe is just a ps2exe wrapper.

## Usage

Download `winutil.exe` from the [latest release](../../releases/latest) and run
it. A UAC prompt is expected — winutil requires admin.

**Note:** Windows Defender sometimes flags ps2exe output as a false positive.
If the file disappears after download, check Windows Security → Protection
history.

Force a rebuild of the current tag:

```
gh workflow run build.yml -f force=true
```

## License

MIT, Copyright (c) 2022 CT Tech Group LLC — see [LICENSE](LICENSE) and
[NOTICE](NOTICE).
