# playground.helloworld

1. File -> New Capsule  
   name it with playground.helloworld

2. open capsule.bxb  
  add followings
```js
  store-sections{
    section (GamesAndFun)
  }

  store-countries{
   // all
   only{
      allow (KR)
    }
  }
```
  add followings to runtime-flags { .. }  
```js
    // add below for error correction
    no-filtering-with-validation
    modern-default-view-behavior
    use-input-views-for-selection-list-detail
```

3. open resource/en-US/capsule-info.bxb  
   -> add followings:   
```js
  dispatch-name (helloworld)
  search-keywords {
    keyword (hello)
  }
```

4. open resources/en-US/hints.bxb  
   replace hints with followings:  
```js
    hint (ask helloworld to say it)
    hint (ask helloworld to say world)
    hint (ask helloworld to say something)
```
see https://stackoverflow.com/questions/57241026/invoke-specific-action-when-bixby-capsule-launched  
The current en-US dispatch patterns are the following:  

    "with %dispatch-name% ..."
    "in %dispatch-name% ..."
    "ask %dispatch-name% ..."
    "ask %dispatch-name% for ..."
    "ask %dispatch-name% to ..."

The current ko-KR dispatch pattern is the following:

    %dispatch-name% 에서 ...

5. create models/concepts/world.model.bxb  
   . models -> concepts (right click)  
    -> New -> Model  
     . File Type: Model  
     . Template : Text  
  
6. create code/helloWorld.js  
   . code (right click)  
   -> New -> Action JavaScript  
```js
module.exports.function = function helloWorld () {
  return "hello, world"
}
```

7. create models/actions/doHelloWorld.model.bxb  
   . models -> concepts (right click)  
    -> New -> Model (template: Action)  
```js
action (doHelloWorld) {

  output (world)
  type (Calculation)
}
```
8. create resources/base/views/helloWorld.view.bxb  
   . resources -> base -> views (right click)  
    -> New -> View  
   . it's an empty file  

9. add followings to resources/base/endpoints.bxb  
```js
endpoints {
  // action과 그에 맞는 자바스크립트를 매핑
  action-endpoints {
    action-endpoint (doHelloWorld) {
      local-endpoint ("helloWorld.js")
    }
  }
}
```
10. open resources/en-US/training  
    add followings, set goal as world, and "Compile NL Model"  

    say it  

11. run Bixby Emulator  
  put "say it" to input terminal, and "Run NL"  
