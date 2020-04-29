# JavaScript

## local

`$ hexo s`  
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/javascript/

doc\source\_data\navigation.yaml

## hexo 

[commands](https://hexo.io/zh-tw/docs/commands.html)  
[hexo-theme-doc](https://github.com/zalando-incubator/hexo-theme-doc)  

_config.yaml

```js
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
root: /javascript

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
    type: git
    repository: https://github.com/JacobHsu/javascript
    branch: gh-pages
```

ERROR Deployer not found: git
`npm install hexo-deployer-git --save`  

`$doc> hexo g`
`$doc> hexo d`

## Notes

[【Hexo異常】fatal: in unpopulated submodule '.deploy_git'](https://blog.csdn.net/nomasp/article/details/79504699) 

把它刪掉，然後重新生成和部署。
`rm -rf .deploy_git`  
`hexo g`  
`hexo d`  
