# Node Gyp with Visual Studio 2017 on Windows
*Note: You can also just `npm install --global windows-build-tools`.*

Thanks to [@joaocgreis](https://github.com/joaocgreis)'s [comment](https://github.com/nodejs/node-gyp/issues/1056#issuecomment-285131148) on GitHub.

### Python
Install Python 2.7 via [chocolatey](https://chocolatey.org): `choco install python2`  

Or from [python.org](https://www.python.org/downloads/release/python-2713/).

### Visual Studio
1. Download and install [Visual Studio 2017](https://www.visualstudio.com/)
2. In the installer, click on the "Individual Components" tab
3. Under "Compilers, Build Tools, and Runtimes" select `VC++ 2017 v141 toolset (x86,x64)`
4. Under "Development Activities" select `Visual Studio C++ core features`
5. Under "SDKs, libraries, and frameworks" select `Windows 10 SDK` (any version, I picked `10.0.10240.0`)

### NPM
Add the following to your `.npmrc` in your `$HOME` directory:  

*Note: I'm using the default Chocolatey installation path for Python.*

```text
msvs_version=2017
python=C:\Python27\python.exe
```

### Test

```bash
mkdir test
cd test
npm init --yes
npm install --save bcrypt
```

In `test.js`:

```javascript
const bcrypt = require('bcrypt');

const password = 'password';
const salt = bcrypt.genSaltSync(10);
const hash = bcrypt.hashSync(password, salt);

console.log(hash);
```

Run `node test.js`
