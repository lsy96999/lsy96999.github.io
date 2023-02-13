---
layout: post
title:  "JS)js-console"
date:   2023-02-13 14:28:18 +0900
categories: js
---
환경별 JS 콘솔 찍기  
isProduct(), 운영 환경이면 info 레벨이 기본, 아니면 log가 기본

{% highlight js %}
//해당 환경에 맞게 구현
function isProduct(){
    return true;
}

class LogHelper{
    _LEVEL_LOG = 0;
    _LEVEL_INFO = 1;
    _LEVEL_WARN = 2;
    _LEVEL_ERROR = 3;

    _prefix;
    _logHeleprState = {
        level: isProduct() ? this._LEVEL_INFO : this._LEVEL_LOG,
    };

    constructor(prefix, option) {
        this._prefix = prefix;
        this._logHeleprState = {...this._logHeleprState, ...option};
    }

    get log(){return this._logSub(this._LEVEL_LOG);}
    get info(){return this._logSub(this._LEVEL_INFO);}
    get warn(){return this._logSub(this._LEVEL_WARN);}
    get error(){return this._logSub(this._LEVEL_ERROR);}

    _logSub(level){
        let type;
        let func;
        if(level === this._LEVEL_LOG){
            type = '';
            func = console.log;
        } else if(level === this._LEVEL_INFO){
            type = '[Info]';
            func = console.info;
        } else if(level === this._LEVEL_WARN){
            type = '[Warn]';
            func = console.warn;
        } else if(level === this._LEVEL_ERROR){
            type = '[Error]';
            func = console.error;
        }

        if(this._logHeleprState.level <= level)
            return func.bind(window.console, `${type}[${this._prefix}][${this._getTime()}]`)
        else
            return ()=>{}
    }

    _getTime(){
        return new Date().toTimeString().split(' ')[0]
    }

    levelToLOG(){
        this._logHeleprState.level = this._LEVEL_LOG;
    }
    levelToINFO(){
        this._logHeleprState.level = this._LEVEL_INFO;
    }
    levelToWARN(){
        this._logHeleprState.level = this._LEVEL_WARN;
    }
    levelToERROR(){
        this._logHeleprState.level = this._LEVEL_ERROR;
    }
}
{% endhighlight %}


useCase
{% highlight js %}
const lh = new LogHelper('Example')
lh.log('hello-world')
//[Example][15:04:57] hello-world
{% endhighlight %}