# JavaScript

# hexo 

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
