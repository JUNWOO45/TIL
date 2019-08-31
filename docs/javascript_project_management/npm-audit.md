<h1>
  npm audit
</h1>



npm audit은, 사용하는 npm모듈의 취약점을 검사해주는 기능입니다.

npm install을 했을 때, 여러 경고가 떴습니다.

마지막에 이런 문구가 있었는데요.

```
npm notice created a lockfile as package-lock.json. You should commit this file.
added 847 packages from 586 contributors and audited 9751 packages in 12.384s
found 8 vulnerabilities (4 moderate, 4 high)
```

취약점이 발견되었다네요...

우선 처음으로 npm audit을 사용해봅니당

```
$ npm audit
```

결과가 보기 쉽게 표로 나옵니다.

해결법도 표 위에 나오기도 하네요..



```
# Run  npm install --save-dev css-loader@2.1.1  to resolve 2 vulnerabilities
SEMVER WARNING: Recommended action is a potentially breaking change
```

모듈을 업데이트해서 취약점을 해결할때 호환성이 깨진 업데이트가 있으면 이런 문구도 나온다고합니다.



해결을 위해 npm audit fix를 실행해봅니다.

```
$ npm audit fix
```

결과는...

```
added 2 packages from 5 contributors and updated 2 packages in 2.731s
fixed 6 of 8 vulnerabilities in 9751 scanned packages
  1 package update for 2 vulns involved breaking changes
  (use `npm audit fix --force` to install breaking changes; or refer to `npm audit` for steps to fix these manually)
```

뭐가 잘 되기도하고, 잘 안된부분도 있나봅니다.

```
$ npm audit fix --force
```

를 실행하라니.. 해줍니다.

```
npm WARN using --force I sure hope you know what you are doing.
```

실행을 하니깐 이런 무시무시한 경고가 뜨네요.

이런건 실행전에 알려주면 더 조심할텐데;;

```
fixed 2 of 2 vulnerabilities in 9751 scanned packages
  1 package update for 2 vulns involved breaking changes
  (installed due to `--force` option)
```

잘 해결된듯합니다..!

