# `node-web-audio-api-rs`

> Nodejs bindings for [`orottier/web-audio-api-rs`](https://github.com/orottier/web-audio-api-rs/) using [`napi-rs`](https://github.com/napi-rs/napi-rs/)

## Install (@todo)

```
npm install node-web-audio-api-rs
```

## Example

```js
const { AudioContext, OscillatorNode, GainNode } = require('node-web-audio-api-rs');

const audioContext = new AudioContext();

setInterval(() => {
  const now = audioContext.currentTime;

  const env = new GainNode(audioContext);
  env.connect(audioContext.destination);
  env.gain.value = 0;
  env.gain.setValueAtTime(0, now);
  env.gain.linearRampToValueAtTime(1, now + 0.02);
  env.gain.exponentialRampToValueAtTime(0.0001, now + 1);

  const osc = new OscillatorNode(audioContext);
  osc.frequency.value = 200 + Math.random() * 2800;
  osc.connect(env);
  osc.start(now);
  osc.stop(now + 1);
}, 50);
```

To run this example, install `rust` toolchain (cf. [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)), then:

```sh
git clone https://github.com/b-ma/node-web-audio-api-rs.git
cd node-web-audio-api-rs
npm install
npm run build
node simple-test.js
```

## Roadmap

- Make a few nodes work properly with clean and predictable code
- Generate bindings from IDL [https://webaudio.github.io/web-audio-api/#idl-index](https://webaudio.github.io/web-audio-api/#idl-index)
- Publish on `npm` with binaries
- Implement prototype chain (?)
- Follow developments of `web-audio-api-rs`

## License

This project is licensed under the [MIT license](./LICENSE).
