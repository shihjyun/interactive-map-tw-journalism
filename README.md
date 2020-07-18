*Looking for a shareable component template? Go here --> [sveltejs/component-template](https://github.com/sveltejs/component-template)*

---

# svelte app

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.


## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```


## Deploying to the web

### With [now](https://zeit.co/now)

Install `now` if you haven't already:

```bash
npm install -g now
```

Then, from within your project folder:

```bash
cd public
now deploy --name my-project
```

As an alternative, use the [Now desktop client](https://zeit.co/download) and simply drag the unzipped project folder to the taskbar icon.

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```

```
interactive-map-tw-journalism
├─ .git
│  ├─ COMMIT_EDITMSG
│  ├─ config
│  ├─ description
│  ├─ FETCH_HEAD
│  ├─ HEAD
│  ├─ hooks
│  │  ├─ applypatch-msg.sample
│  │  ├─ commit-msg.sample
│  │  ├─ fsmonitor-watchman.sample
│  │  ├─ post-update.sample
│  │  ├─ pre-applypatch.sample
│  │  ├─ pre-commit.sample
│  │  ├─ pre-push.sample
│  │  ├─ pre-rebase.sample
│  │  ├─ pre-receive.sample
│  │  ├─ prepare-commit-msg.sample
│  │  └─ update.sample
│  ├─ index
│  ├─ info
│  │  └─ exclude
│  ├─ logs
│  │  ├─ HEAD
│  │  └─ refs
│  │     ├─ heads
│  │     │  └─ master
│  │     └─ remotes
│  │        └─ origin
│  │           └─ master
│  ├─ objects
│  │  ├─ 02
│  │  │  └─ 82c1323583fde668789f17e9a976caa8a31646
│  │  ├─ 07
│  │  │  └─ 28705d282cc657ad902f021cd6101da27d112e
│  │  ├─ 09
│  │  │  └─ daa3b093db18373fbeb0b83e2cdc26bdebf696
│  │  ├─ 0a
│  │  │  └─ b362db5e0d7f154051c467e8e1e4b29dc6aad7
│  │  ├─ 0b
│  │  │  └─ fd8af2c97337c809cb778ba45fc306148fe5fe
│  │  ├─ 0c
│  │  │  ├─ 3743b4dd07b4c8569ccfbe88dfe73c5f22f1a7
│  │  │  └─ a40f5fc60b09c98521b4864fe2cb80fcded9cf
│  │  ├─ 0e
│  │  │  └─ 0eed81cc0c9f57d86d4c65a918576cb822d2bb
│  │  ├─ 16
│  │  │  └─ d855f5dc4368b6170d64a5dd4d9d4a3775c373
│  │  ├─ 1b
│  │  │  └─ b6e4727f71526067180a912b6812dec6bc0610
│  │  ├─ 23
│  │  │  └─ 4b0742edd75d4d079b0e33f4e4870ef4c44240
│  │  ├─ 2c
│  │  │  └─ fedab754b04e8820a3b678560e10885d005ea0
│  │  ├─ 30
│  │  │  └─ fc28b6063dd9a276fa22ee2f93af40a6118ffe
│  │  ├─ 31
│  │  │  └─ 23d8a5d4e81e4c04d3c2b2cfd3ba770b55d151
│  │  ├─ 32
│  │  │  └─ 199623298339a46968533f7c1baa6ac8a5aead
│  │  ├─ 3b
│  │  │  └─ bc63cca6de5117657ca45a44073fae35d8acaf
│  │  ├─ 3e
│  │  │  └─ 8a3e3091011bced376cf2e9e6c304e5cd0fda3
│  │  ├─ 3f
│  │  │  └─ 7ac0c40bb6c89b57a35b2463db58f06e2057f2
│  │  ├─ 40
│  │  │  └─ bc899bf37653103d9abc3bede978a34625471a
│  │  ├─ 41
│  │  │  └─ bb34f13d6f8d6b5a10b8a6e21dbc416f55a8a0
│  │  ├─ 43
│  │  │  └─ bd43cfa180cab8b57f236f63654e6ddd892ae5
│  │  ├─ 48
│  │  │  └─ d13bfb59dcce0a51e7e667991e2d2ffd6ebc82
│  │  ├─ 4c
│  │  │  └─ a2d52f7b765554b1c5596cfe536f54b4552b38
│  │  ├─ 4e
│  │  │  └─ 5f2024127777d5da8f1023783d65f458513bf9
│  │  ├─ 50
│  │  │  └─ fb13118b999fdbb7ae923a16b77a83adb025e7
│  │  ├─ 54
│  │  │  └─ 931a5fe6fc3f71caa5575d9a94971c76be60e7
│  │  ├─ 57
│  │  │  └─ 7d6305c4f3780df4e06e274e753ab71ecdfe4f
│  │  ├─ 5f
│  │  │  ├─ aa6853ab5ecace4d2aaa92dad84550a9b68de8
│  │  │  └─ b633aaad8c2c738f09a4f5add0474713d5f65c
│  │  ├─ 64
│  │  │  └─ 71862a5f4b13f9ac8007e5a2cf54bca8b645dc
│  │  ├─ 6d
│  │  │  └─ 2dc22c138db5fb3b6eb9d4b54acba559a6745d
│  │  ├─ 71
│  │  │  └─ 19c2f9e9e409e351ffb9c82c511daf83346afc
│  │  ├─ 76
│  │  │  └─ 45507f6ad6bcc860d7a0d2c6a01896ecb5c7f5
│  │  ├─ 79
│  │  │  └─ c50caa4c67e87e5f603e3c444a7c92f8d2668e
│  │  ├─ 7b
│  │  │  ├─ e1552fd07d5d59332e888075a2257bf1a42ae0
│  │  │  └─ e8f92cf08ce90d272000e4ed67ac65b57d9452
│  │  ├─ 7e
│  │  │  └─ c34ef68bfaeba882f24c9bf7068fa14cf20bcc
│  │  ├─ 87
│  │  │  ├─ b55719e4a67eaf9c43be25103fb85bf7254392
│  │  │  └─ eef83715fd9fdba6156a2f2f03f0cf1cef1d6d
│  │  ├─ 90
│  │  │  └─ 7a64655e784b78bbf0ef4d80d4da315699fcb0
│  │  ├─ 91
│  │  │  └─ 410629c5c8a902445f0f37252d5ca32b37c02d
│  │  ├─ 92
│  │  │  └─ 30b48f2f6ac6a2928fb41a29880eb40c9a1817
│  │  ├─ 95
│  │  │  └─ 1b6b0f4968a4c1b8beeb68413f0a9d867cbe90
│  │  ├─ 96
│  │  │  └─ 2ed88bab357df29a30266f8d48c37f000ad06c
│  │  ├─ 98
│  │  │  └─ 4572f4af1d0a87c5108354ff3e1574671ce0a1
│  │  ├─ 99
│  │  │  ├─ 1c8706639085c3b0f49a6edfa92aa3cfaf1b00
│  │  │  ├─ 27462ba00977b77e8b37e0e2d2c8d78da0e865
│  │  │  └─ 62ebff8147f669982d30e0245c1a1c5db2cfcf
│  │  ├─ a1
│  │  │  ├─ 89f359d442102a904ad9a0d5dc7c2f6fb70d04
│  │  │  └─ f35843304d8473b40a8e82e581b51b09562f7f
│  │  ├─ a4
│  │  │  └─ 9f684e003ed265fa4ae5c8b9a0ca2cce87ac92
│  │  ├─ a6
│  │  │  └─ 6ac795b297586596c2834700a4e06fcce2cf25
│  │  ├─ ab
│  │  │  └─ 0fbc9d2156ae3babb1943ab25177e5691b465c
│  │  ├─ ad
│  │  │  └─ 66f396bb3d938e07fcc4263a7e01e8eb672d48
│  │  ├─ b0
│  │  │  ├─ 66905599e6af35b68835aae6a8e520c22c6d1d
│  │  │  └─ 99ce95f443ed73e7f46a1a1845a040d0a33f16
│  │  ├─ bc
│  │  │  └─ 44a7170e65f15a5e784f25f4122528afe8b6d4
│  │  ├─ be
│  │  │  └─ 140de5eeaf88ecb4e7081b0b7b43c3d1c214f6
│  │  ├─ c3
│  │  │  └─ 09f9c069520726ccf5fbcab4e0d0701cc5d139
│  │  ├─ c4
│  │  │  └─ 1c38344a1ef5b5ee0a68231e70bababa969de7
│  │  ├─ c6
│  │  │  └─ f6d96436343da5d0db8cc29056875dc5adeaa1
│  │  ├─ c8
│  │  │  └─ 86666b50250d683d7b422ffa2a1f2fc08a41e7
│  │  ├─ ca
│  │  │  └─ 5aac2ccd04fe97ac8a4f4f9c19e88015eaf39b
│  │  ├─ cb
│  │  │  └─ b4903b3b5e656e4b19929dc984bf0f3194dd0d
│  │  ├─ cd
│  │  │  └─ 5bb9ac099ea49a84db908f97254d93800b69e2
│  │  ├─ ce
│  │  │  └─ 3c9ebab55bbcfb3dae3733df62e5d1107b0373
│  │  ├─ cf
│  │  │  └─ 94ec6eb6992e23ac929f5271a768982f6a695c
│  │  ├─ d4
│  │  │  └─ 94bce7dd9b9d02669acf4419f6a719a2525f2b
│  │  ├─ d5
│  │  │  ├─ 82ea6660ca9ade6b7ad23550ce8ea94cea51ef
│  │  │  └─ ac23559747318966ba03a686cee7a29d0165b5
│  │  ├─ da
│  │  │  └─ 93220bc34984be11385afbbe6cd044e7b455eb
│  │  ├─ db
│  │  │  └─ 6fd64f6ded56ecb03ef30c3a3e9d4455113108
│  │  ├─ dd
│  │  │  └─ c60e57fee1acd49ab1efe5027c1e6c59990af3
│  │  ├─ de
│  │  │  └─ aa73433b7ee9caab5db11af73a043b0ba8e92a
│  │  ├─ df
│  │  │  └─ c88316b5c49ab7c6d77ef1f91346a4c34c47fb
│  │  ├─ e8
│  │  │  └─ 26692ca6b0e49c3eef8f7a8bf0ad3bfd1e79d4
│  │  ├─ ea
│  │  │  └─ 307a35242f83c1282c304fda7bc744482f6001
│  │  ├─ ee
│  │  │  └─ 90d17ea06e43b136482e5e8a2d1da1e87c20a1
│  │  ├─ f1
│  │  │  └─ aba6d0c0027be67e1b940bf2904be4f5f150f4
│  │  ├─ f6
│  │  │  └─ f4f385459f4bbaa828f207295dd320b0d8a329
│  │  ├─ fb
│  │  │  ├─ c388eda595338b0f45ea89adcbaa7b9a43a1cf
│  │  │  └─ da06858209e4b87129873e6ba48fb9a5084b7a
│  │  ├─ fd
│  │  │  └─ b28462e0ab6714501ca24b66c089503c6a0b23
│  │  ├─ info
│  │  └─ pack
│  ├─ ORIG_HEAD
│  ├─ refs
│  │  ├─ heads
│  │  │  └─ master
│  │  ├─ remotes
│  │  │  └─ origin
│  │  │     └─ master
│  │  └─ tags
│  └─ sourcetreeconfig.json
├─ .gitignore
├─ package-lock.json
├─ package.json
├─ public
│  ├─ data
│  │  ├─ tw_county.json
│  │  └─ tw_town.json
│  ├─ global.css
│  └─ index.html
├─ README.md
├─ rollup.config.js
└─ src
   ├─ App.svelte
   ├─ components
   │  ├─ InteractiveTool.svelte
   │  └─ TaiwanMap.svelte
   ├─ helper
   │  └─ gs2json.js
   ├─ main.js
   └─ stores
      └─ MapInfo.js

```