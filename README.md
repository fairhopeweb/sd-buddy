# ![Square30x30Logo](https://user-images.githubusercontent.com/17433578/189560882-51ea2b07-f9a0-4798-92e5-4779592bc6c4.png) Stable Diffusion Buddy

Companion desktop app for the self-hosted M1 Mac version of [Stable Diffusion](https://github.com/magnusviri/stable-diffusion).

It is intended to be a lazier way to generate images, by allowing you to focus on writing prompts instead of messing with the command line.

![Stable Diffusion Buddy v0.8.0](https://user-images.githubusercontent.com/17433578/190299350-cf862c0c-996c-49c2-805d-30f9194c98f1.png)

Behind the scenes it executes this command in your local Stable Diffusion directory:

```shell
python scripts/txt2img.py \
  --prompt "a red juicy apple floating in outer space, like a planet" \
  --n_samples 1 --n_iter 1 --plms --ddim_steps 10 --H 512 --W 512 --seed 42
```

**Important Note 1** It's a WIP, so check back often. For now it's barely a step above running the command manually, but I have a lot of things in mind (see the [wishlist](#wishlist) below) that should make my life easier when generating images with Stable Diffusion.

**Important Note 2** This is a spur-of-the-moment, passion project that scratches my own itch. As a result, I feel zero pressure or desire to satisfy anyone else's wishlist. So if you feel it lacks anything YOU want, or I'm moving too slowly, go ahead and fork the repo and build your own thing.

## Stack

The app is built with:

- Back-end: [Tauri](https://tauri.app/)
- Front-end: [Svelte](https://svelte.dev/)
- UI: [Tailwind CSS](https://tailwindcss.com/)
- Various packages (check `package.json`)

## Prerequisites

- An M1 Mac.

- Follow this [excellent guide](https://replicate.com/blog/run-stable-diffusion-on-m1-mac) or this equally excellent [Twitter thread](https://twitter.com/levelsio/status/1565731907664478209) to install Stable Diffusion on your M1 Mac.

- Make sure the program runs without errors and it can generate images by running the above command manually, before using the app. _The app doesn't have a lot of error checking built in, so try not to abuse it 🙂_

## Features

The first publicly-available version is pretty thin on features. My goal was to provide a basic UI around the CLI command.

- <label><input type="checkbox" checked /> Register and persist the location of the Stable Diffusion directory.</label>
- <label><input type="checkbox" checked /> Clickable links for the Stable Diffusion project and output directories.</label>
- <label><input type="checkbox" checked /> Generation parameters: **prompt** (`--prompt`), **steps** (`--ddim_steps`), **scale** (`--scale`), **batch count** (`--n_iter`), **batch size** (`--n_samples`), image **height** (`--H`) and **width** (`--W`), **seed** (`--seed`).</label>
- <label><input type="checkbox" checked /> Generate multiple images with the same parameters, in sequence.</label>
- <label><input type="checkbox" checked /> Use a random seed for each generation.</label>
- <label><input type="checkbox" checked /> Parameter matrix (aka parametric prompts). Use variables prefixed with "$" to trigger a set of inputs for each variable where you can list comma-separated parameters. You can then generate the entire batch of prompt combinations with one click.</label>
- <label><input type="checkbox" checked /> **NEW** Prompt queue. Push prompts to a queue so they can be generated in sequence. Delete queue items, or mark them as skipped.</label>
- <label><input type="checkbox" checked /> Real-time duration timer.</label>
- <label><input type="checkbox" checked /> Display the output of the command and click it to copy to the clipboard.</label>
- <label><input type="checkbox" checked /> Display the generated image at 512x512.</label>
- <label><input type="checkbox" checked /> Delete a run from history.</label>
- <label><input type="checkbox" checked /> A history of previous runs is displayed below the form.</label>
- <label><input type="checkbox" checked /> Thumbnails for the generated images (click an image to open it in the associated program).</label>
- <label><input type="checkbox" checked /> Links to the generated images (opens it in the associated program).</label>
- <label><input type="checkbox" checked /> Click a previous run to reuse the prompt & all the generation parameters.</label>
- <label><input type="checkbox" checked /> Each run contains generation parameters metadata.</label>
- <label><input type="checkbox" checked /> Gallery section which shows all the generated images in a simple grid. Has controls to filter by prompt fragment, sort by generated timestamp, and change thumbnail size.</label>
- <label><input type="checkbox" checked /> Keyboard shortcuts for quitting the app, copy/paste, etc.</label>

## Download

Download the compiled app in `.dmg` format from the [Releases](https://github.com/breadthe/sd-buddy/releases) page.

The app is unsigned so you will get a security message when you open it the first time.

![2022-09-11-sd-buddy-security-1](https://user-images.githubusercontent.com/17433578/189551753-e2f35ee8-fac5-411f-8d31-d3ab7d55e651.png)

Go to System Preferences > Security & Privacy > General, and click Open Anyway.

![2022-09-11-sd-buddy-security-2](https://user-images.githubusercontent.com/17433578/189551759-8bf4df8c-00fb-4e2f-9e81-d2693ad657e5.png)

Open the app again and this time you'll get a different security warning. Click Open and you should be set.

![2022-09-11-sd-buddy-security-3](https://user-images.githubusercontent.com/17433578/189551763-c49bf16e-82b5-496a-a81d-a48ef3329af7.png)

## Windows and Linux builds

For a short time there were Linux and Windows builds available. I disabled those for several reasons.

1. This project is optimized around the M1 Mac flavor of Stable Diffusion.
2. Even though Stable Diffusion can be installed on Windows, certain "magic" I employed around determining which is the last generated image dictates that this will remain a Mac build for now. I'll have to change this at some point since it's not ideal.
3. The "magic" mentioned on #2 may actually work in Linux but I don't have a way to test it. If you do have a Linux environment with Stable Diffusion installed and are willing to build this app yourself, please give it a try and let me know in a new Discussions topic.
4. In the end I kept only the Mac build because it makes GitHub Actions CI faster to have 1 build instead of 3.

## Building the app

In addition to the above, if you want to build the Mac binary yourself, first install the [Tauri environment + CLI](https://tauri.app/v1/guides/getting-started/prerequisites) (including the Rust CLI + Cargo), then clone this repo and run:

```shell
npm install

# dev mode
cargo tauri dev

# build the production app
cargo tauri build
```

## Generating app icons

Follow the official Tauri [icons guide](https://tauri.app/v1/guides/features/icons).

```shell
npx @tauri-apps/tauricon src/assets/sd-buddy-logo.png
```

## Alpha status

Be aware that if the current version looks like v0.x.x the app is in "alpha" state, meaning that things can and will change drastically between versions. This includes breaking changes, regressions, or new bugs.

[](#wishlist)

## Wishlist

I'll tackle these in whatever order I feel is a priority for how I use Stable Diffusion.

- A gallery of generated images.
- Light/dark mode.
- UI improvements including a Help section.
- Configurable output folder.
- Embed the metadata in the generated image, optionally. A similar thing can be done by saving the generation parameters to a text file with the same name as the image. Follow the changes in my [txt2img.py gist](https://gist.github.com/breadthe/e0fda9f766c691a2cf4533f1da65560e).
- Support `img2img.py` as in `python scripts/img2img.py --prompt "a red juicy apple floating in outer space, like a planet" --init-img apple-input.jpg --strength 0.8 --skip_grid --n_samples 1`.

In addition, I need to sort out various small details around developing with Tauri, such as global keyboard shortcuts for common actions such as quitting the app, enabling copy/paste in text boxes, and narrowing down the file/directory operations scope to the settings folder.

[](#known_issues)

## Known issues

1. The `tauri.allowlist.fs.scope` key in `tauri.conf.json`. This essentially defines what file system locations the `fs` command is allowed to touch. Currently it is set to `**` which means everywhere. Since `fs` is used only by the `tauri-settings` package to create and write to `settings.json`, I'm not worried about it. Nevertheless, I'd like to limit it to just the location it needs once I discover the correct string pattern for that option.

2. The current (v0.3.0) image thumbnail rendering feature suffers from an issue stemming from the way I implemented it. Essentially when the program completes, I run a Rust function that executes a system command (`find` + arguments) to retrieve the name of the newest image in the output folder that was created during the timeframe in which the run completed. Then I read the image contents from disk as binary data and convert it to a base64 string to be rendered on the front-end. Unfortunately it seems that the Stable Diffusion python command sometimes overwrites files. So what used to be `grid-0032.jpg` from a previous run is also the same for a new run. This causes the generated thumbnails to look the same, since the metadata embedded with each run to points to the same location. **Workaround** I think my problem appeared because I was deleting images from disk that I didn't like, thus creating gaps. The SD command likes to back-fill those gaps but it also overwrites images that I hadn't deleted.

3. Setting _Samples_ to anything other than 1 crashes the Python script with this message `failed assertion [MPSTemporaryNDArray initWithDevice:descriptor:] Error: product of dimension sizes > 2**31' /opt/homebrew/Cellar/python@3.10/3.10.6_2/Frameworks/Python.framework/Versions/3.10/lib/python3.10/multiprocessing/resource_tracker.py:224: UserWarning: resource_tracker: There appear to be 1 leaked semaphore objects to clean up at shutdown`.

4. The queue cannot be stopped currently (v0.11.0) while it's processing. There is also a minor issue which prevents the same prompt matrix from being added more than once, which would actually be a feature if it was consistent with how simple prompts behave (they can be added multiple times).

## Troubleshooting

### Image generation fails when disconnected from the internet

While SD Buddy is completely offline and doesn't need the internet to function, it appears that the Stable Diffusion installation does in fact need an internet connection. I first ran into this problem while on plane in airplane mode. I haven't researched why that's the case. You can verify by putting your computer in airplane mode (or disconnecting from the internet) and running the Python script manually.

### ModuleNotFoundError: no module named "ldm"

If you receive this error when running `img2img` follow [these instructions](https://github.com/CompVis/stable-diffusion/issues/160).

In `/path/to/stable-diffusion/scripts/img2img.py` add this line above the `ldm` imports:

```python
sys.path.append(os.path.join(os.path.dirname(__file__), "..")) # add this line
from ldm.util import instantiate_from_config
from ldm.models.diffusion.ddim import DDIMSampler
from ldm.models.diffusion.plms import PLMSSampler
```

### UserWarning: resource_tracker: There appear to be 1 leaked semaphore objects to clean up at shutdown

Enforce a small number of samples (`--n_iter`, `--n_samples`), ideally 1. Example:

```shell
python3 scripts/img2img.py --prompt "A fantasy landscape, trending on artstation" --init-img sketch-mountains-input.jpg --strength 0.8 --n_iter 1 --n_samples 1
```

## Security FAQ

- **How secure is the app?** It is strictly a local app that doesn't communicate with the network. Tauri disables all system APIs by default. I've enabled the minimum necessary system APIs to allow it to function.
- **How do I know it's not communicating with the internet?** Use a network inspector tool to analyze the traffic.
- **How do I know it doesn't do nefarious things on my computer?** It's open source. Feel empowered to inspect the source code and build it yourself.
- **Why is the app unsigned?** Currently I don't have an Apple developer account because I'm not paying Apple for the privilege since I'm not making any money from this app or any other. When this changes, I would love to be able to sign my apps. If you want to contribute towards this goal, a [sponsorship](https://github.com/sponsors/breadthe) is very much appreciated.

## Contributing

At this time **Stable Diffusion Buddy** is **not** open to contribution. You may create issues but there's absolutely no guarantee I will tackle or even glance at them.

If you feel strongly that you want to contribute, please focus on these areas:

- Submit fixes for critical bugs you have encountered
- Submit PRs that handle the [known issues](#known_issues) listed above
- Improvements on the Tauri side (I'm still a noob, please teach me)

New feature requests that are not on the [wishlist](#wishlist) will probably fall on deaf ears, unless it's something that I personally like, or has been explained really well in [Discussions](https://github.com/breadthe/sd-buddy/discussions).

Here's an example of a very [thoughtful PR](https://github.com/breadthe/sd-buddy/pull/2) by [Swyx](https://github.com/sw-yx) that fixed actual issues. I added those myself manually since by that time the code had shifted. So use that as a model and all will be good.

## License

Until I find the appropriate license to attach, please consider and abide by the following terms of use.

**Stable Diffusion Buddy** is provided as-is without any guarantees. I assume no liabilities from any potential harm (physical, financial, or otherwise) from using it. In other words, _use at your own risk_.

**Stable Diffusion Buddy** is open source and free for _personal use_.

You may not use **Stable Diffusion Buddy** for _any_ commercial purpose. That means you may not sell or profit in any way from the compiled app, from compiling the app yourself, from the source code, or a fork of it. The images generated by using this app do not fall under these limitations for obvious reasons.

Unless it's strictly for personal use (on your machine), when forking the source code and/or rebuilding the binary please provide attribution and a link to this repo in a README file.
