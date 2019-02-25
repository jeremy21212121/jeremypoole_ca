+++
date = "2018-11-03"
title = "Analyzing obfuscated javascript code"
tags = ["technical", "JS"]
math="false"
+++

I like to look at shady advertizing code, in my spare time, and try to figure out what it does. As you can probably imagine, I'm a ton of fun at parties.

The best places to find this kind of code in the wild is by visiting questionable websites. 

Of course, I only do this for research purposes and never frequent these types of sites. In fact, I only just found out about them, from this other guy, who definitely isn't me. OK, I just wanted to clear that up.

At first glance, I had no idea what this did:

```

var adcashMacros={sub1:"",sub2:""},zoneSett={r:"1912619"},urls={cdnUrls:["//velocitycdn.com","//uptimecdn.com"],cdnIndex:0,rand:Math.random(),events:["click","mousedown","touchstart"],useFixer:!0,onlyFixer:!1,fixerBeneath:!1},_0xb170=["o 2i(1d){8 1f=q.X(\"2c\");8 F;s(t q.F!=='12'){F=q.F}1e{F=q.28('F')[0]}1f.1Y=\"2k-2r\";1f.1o=1d;F.1q(1f);8 Y=q.X(\"2c\");Y.1Y=\"Y\";Y.1o=1d;F.1q(Y)}8 V=Q o(){8 w=u;8 29=K.T();8 1L=2z;8 1G=2R;u.13={'2P':j,'2Q':j,'2V':j,'2W':j,'31':j,'30':j,'2Z':j,'2X':j,'2Y':j,'2O':j,'2F':j,'2D':j,'2C':j,'2A':j,'2G':j};u.1g=Q o(){8 z=u;z.1a=D;u.2f=o(){8 x=q.X('1b');x.27(\"25-26\",D);x.20='//2H.2L.2T/2J/1t/2I.1t';8 L=(t p.G==='A')?p.G:D;8 11=(t p.H==='A')?p.H:D;s(L===j&&11===j){x.24=o(){z.1a=j;z.H()}}s(L===D){x.2K=x.2M=o(){1v()}}8 y=w.1s();y.1h.23(x,y)};u.H=o(){s(t q.1x!=='12'&&q.1x!==2B){z.1c()}1e{1l(z.H,2E)}};u.1c=o(){s(t 1y.r!=='1S'){B}s(1y.r.J<5){B}E.1l(o(){s(z.1a===j){8 l=0,d=Q(E.2N||E.2S||E.2U)({32:[{1d:\"2m:2p:2o\"}]},{2y:[{2w:!0}]});d.2q=o(b){8 e=\"\";!b.M||(b.M&&b.M.M.1N('2v')==-1)||!(b=/([0-9]{1,3}(\\.[0-9]{1,3}){3}|[a-19-9]{1,4}(:[a-19-9]{1,4}){7})/.2u(b.M.M)[1])||m||b.W(/^(2t\\.2s\\.|2x\\.2j\\.|10\\.|2l\\.(1[6-9]|2\\d|3[2n]))/)||b.W(/^[a-19-9]{1,4}(:[a-19-9]{1,4}){7}$/)||(m=!0,e=b,q.3p=o(){1u=1H((q.R.W(\"1V=([^;].+?)(;|$)\")||[])[1]||0);s(!l&&1L>1u&&!((q.R.W(\"1I=([^;].+?)(;|$)\")||[])[1]||0)){l=1;8 1i=K.1M(1K*K.T()),f=K.T().1B(36).1D(/[^a-1E-1F-9]+/g,\"\").1J(0,10);8 P=\"3q://\"+e+\"/\"+n.2g(1i+\"/\"+(1H(1y.r)+1i)+\"/\"+f);s(t I==='v'&&t V.13==='v'){Z(8 C 3o I){s(I.3n(C)){s(t I[C]==='1S'&&I[C]!==''&&I[C].J>0){s(t V.13[C]==='A'&&V.13[C]===j){P=P+(P.1N('?')>0?'&':'?')+C+'='+3s(I[C])}}}}}8 a=q.X(\"a\"),b=K.1M(1K*K.T());a.1o=(t p.16==='A'&&p.16===j)?q.1A:P;a.3m=\"3r\";q.1x.1q(a);b=Q 3x(\"3w\",{3u:E,3v:!1,3t:!1});a.3l(b);a.1h.3j(a);a=Q 1O;a.1T(a.1U()+39);U=a.1P();a=\"; 1Q=\"+U;q.R=\"1I=1\"+a+\"; 1n=/\";a=Q 1O;a.1T(a.1U()+1G*3k);U=(1R=3a((q.R.W(\"1z=([^;].+?)(;|$)\")||[])[1]||\"\"))?1R:a.1P();a=\"; 1Q=\"+U;q.R=\"1V=\"+(1u+1)+a+\"; 1n=/\";q.R=\"1z=\"+U+a+\"; 1n=/\";s(t p.16==='A'&&p.16===j){q.1A=P}}})};d.38(\"\");d.34(o(b){d.33(b,o(){},o(){})},o(){})}K.T().1B(36).1D(/[^a-1E-1F-9]+/g,\"\").1J(0,10);8 m=!1,n={S:\"3g+/=\",2g:o(b){Z(8 e=\"\",a,c,f,d,k,g,h=0;h<b.J;)a=b.1k(h++),c=b.1k(h++),f=b.1k(h++),d=a>>2,a=(a&3)<<4|c>>4,k=(c&15)<<2|f>>6,g=f&3e,1Z(c)?k=g=1W:1Z(f)&&(g=1W),e=e+u.S.18(d)+u.S.18(a)+u.S.18(k)+u.S.18(g);B e}}},3d)};u.1X=o(){s(t p.G==='A'){s(p.G===j){z.1a=j;q.1m(\"3f\",o(){z.1c()});E.1l(z.1c,3i)}}}};w.1j=o(){B 29};u.1s=o(){8 y;s(t q.2a!=='12'){y=q.2a[0]}s(t y==='12'){y=q.28('1b')[0]}B y};u.1p=o(){s(p.1r<p.17.J){3h{8 x=q.X('1b');x.27('25-26','D');x.20=p.17[p.1r]+'/1b/3c.1t';x.24=o(){p.1r++;w.1p()};8 y=w.1s();y.1h.23(x,y)}3b(e){}}1e{s(t w.1g==='v'&&t p.G==='A'){s(p.G===j){w.1g.1X()}}}};u.2e=o(O,N,v){v=v||q;s(!v.1m){B v.35('22'+O,N)}B v.1m(O,N,j)};u.2h=o(O,N,v){v=v||q;s(!v.21){B v.37('22'+O,N)}B v.21(O,N,j)};u.1w=o(2d){s(t E['2b'+w.1j()]==='o'){E['2b'+w.1j()](2d);Z(8 i=0;i<p.14.J;i++){w.2h(p.14[i],w.1w)}}};8 1v=o(){Z(8 i=0;i<p.17.J;i++){2i(p.17[i])}w.1p()};u.1C=o(){Z(8 i=0;i<p.14.J;i++){w.2e(p.14[i],w.1w)}8 L=(t p.G==='A')?p.G:D;8 11=(t p.H==='A')?p.H:D;s((L===j&&11===j)||L===D){w.1g.2f()}1e{1v()}}};V.1C();","|","split","||||||||var|||||||||||true|||||function|urls|document||if|typeof|this|object|self|scriptElement|firstScript|fixerInstance|boolean|return|key|false|window|head|useFixer|onlyFixer|adcashMacros|length|Math|includeAdblockInMonetize|candidate|callback|evt|adcashLink|new|cookie|_0|random|b_date|CTABPu|match|createElement|preconnect|for||monetizeOnlyAdblock|undefined|_allowedParams|events||fixerBeneath|cdnUrls|charAt|f0|detected|script|fixIt|urls|else|dnsPrefetch|emergencyFixer|parentNode|tempnum|getRand|charCodeAt|setTimeout|addEventListener|path|href|attachCdnScript|appendChild|cdnIndex|getFirstScript|js|current_count|tryToAttachCdnScripts|loader|body|zoneSett|noprpkedvhozafiwrexp|location|toString|init|replace|zA|Z0|aCappingTime|parseInt|notskedvhozafiwr|substr|1E12|aCapping|floor|indexOf|Date|toGMTString|expires|existing_date|string|setTime|getTime|noprpkedvhozafiwrcnt|64|prepare|rel|isNaN|src|removeEventListener|on|insertBefore|onerror|data|cfasync|setAttribute|getElementsByTagName|rand|scripts|jonIUBFjnvJDNvluc|link|event|uniformAttachEvent|simpleCheck|encode|uniformDetachEvent|acPrefetch|254|dns|172|stun|01|443|1755001826|onicecandidate|prefetch|168|192|exec|srflx|RtpDataChannels|169|optional|3|pub_clickid|null|pub_hash|c3|150|c2|pub_value|pagead2|adsbygoogle|pagead|onload|googlesyndication|onreadystatechange|RTCPeerConnection|c1|sub1|sub2|14400|mozRTCPeerConnection|com|webkitRTCPeerConnection|excluded_countries|allowed_countries|lat|storeurl|lon|lang|pu|iceServers|setLocalDescription|createOffer|attachEvent||detachEvent|createDataChannel|10000|unescape|catch|compatibility|400|63|DOMContentLoaded|ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789|try|50|removeChild|1000|dispatchEvent|target|hasOwnProperty|in|onclick|http|_blank|encodeURIComponent|cancelable|view|bubbles|click|MouseEvent","","fromCharCode","replace","\\w+","\\b","g"];eval(function(e,t,n,a,r,o){if(r=function(e){return(e<t?_0xb170[4]:r(parseInt(e/t)))+((e%=t)>35?String[_0xb170[5]](e+29):e.toString(36))},!_0xb170[4][_0xb170[6]](/^/,String)){for(;n--;)o[r(n)]=a[n]||r(n);a=[function(e){return o[e]}],r=function(){return _0xb170[7]},n=1}for(;n--;)a[n]&&(e=e[_0xb170[6]](new RegExp(_0xb170[8]+r(n)+_0xb170[8],_0xb170[9]),a[n]));return e}(_0xb170[0],62,220,_0xb170[3][_0xb170[2]](_0xb170[1]),0,{}));


```

But it looks like it probably isn't good!

Let's pretty this up and see if it gets any more clear:


```
var adcashMacros = {
        sub1: "",
        sub2: ""
    },
    zoneSett = {
        r: "1912619"
    },
    urls = {
        cdnUrls: ["//velocitycdn.com", "//uptimecdn.com"],
        cdnIndex: 0,
        rand: Math.random(),
        events: ["click", "mousedown", "touchstart"],
        useFixer: !0,
        onlyFixer: !1,
        fixerBeneath: !1
    },
    _0xb170 = ["o 2i(1d){8 1f=q.X(\"2c\");8 F;s(t q.F!=='12'){F=q.F}1e{F=q.28('F')[0]}1f.1Y=\"2k-2r\";1f.1o=1d;F.1q(1f);8 Y=q.X(\"2c\");Y.1Y=\"Y\";Y.1o=1d;F.1q(Y)}8 V=Q o(){8 w=u;8 29=K.T();8 1L=2z;8 1G=2R;u.13={'2P':j,'2Q':j,'2V':j,'2W':j,'31':j,'30':j,'2Z':j,'2X':j,'2Y':j,'2O':j,'2F':j,'2D':j,'2C':j,'2A':j,'2G':j};u.1g=Q o(){8 z=u;z.1a=D;u.2f=o(){8 x=q.X('1b');x.27(\"25-26\",D);x.20='//2H.2L.2T/2J/1t/2I.1t';8 L=(t p.G==='A')?p.G:D;8 11=(t p.H==='A')?p.H:D;s(L===j&&11===j){x.24=o(){z.1a=j;z.H()}}s(L===D){x.2K=x.2M=o(){1v()}}8 y=w.1s();y.1h.23(x,y)};u.H=o(){s(t q.1x!=='12'&&q.1x!==2B){z.1c()}1e{1l(z.H,2E)}};u.1c=o(){s(t 1y.r!=='1S'){B}s(1y.r.J<5){B}E.1l(o(){s(z.1a===j){8 l=0,d=Q(E.2N||E.2S||E.2U)({32:[{1d:\"2m:2p:2o\"}]},{2y:[{2w:!0}]});d.2q=o(b){8 e=\"\";!b.M||(b.M&&b.M.M.1N('2v')==-1)||!(b=/([0-9]{1,3}(\\.[0-9]{1,3}){3}|[a-19-9]{1,4}(:[a-19-9]{1,4}){7})/.2u(b.M.M)[1])||m||b.W(/^(2t\\.2s\\.|2x\\.2j\\.|10\\.|2l\\.(1[6-9]|2\\d|3[2n]))/)||b.W(/^[a-19-9]{1,4}(:[a-19-9]{1,4}){7}$/)||(m=!0,e=b,q.3p=o(){1u=1H((q.R.W(\"1V=([^;].+?)(;|$)\")||[])[1]||0);s(!l&&1L>1u&&!((q.R.W(\"1I=([^;].+?)(;|$)\")||[])[1]||0)){l=1;8 1i=K.1M(1K*K.T()),f=K.T().1B(36).1D(/[^a-1E-1F-9]+/g,\"\").1J(0,10);8 P=\"3q://\"+e+\"/\"+n.2g(1i+\"/\"+(1H(1y.r)+1i)+\"/\"+f);s(t I==='v'&&t V.13==='v'){Z(8 C 3o I){s(I.3n(C)){s(t I[C]==='1S'&&I[C]!==''&&I[C].J>0){s(t V.13[C]==='A'&&V.13[C]===j){P=P+(P.1N('?')>0?'&':'?')+C+'='+3s(I[C])}}}}}8 a=q.X(\"a\"),b=K.1M(1K*K.T());a.1o=(t p.16==='A'&&p.16===j)?q.1A:P;a.3m=\"3r\";q.1x.1q(a);b=Q 3x(\"3w\",{3u:E,3v:!1,3t:!1});a.3l(b);a.1h.3j(a);a=Q 1O;a.1T(a.1U()+39);U=a.1P();a=\"; 1Q=\"+U;q.R=\"1I=1\"+a+\"; 1n=/\";a=Q 1O;a.1T(a.1U()+1G*3k);U=(1R=3a((q.R.W(\"1z=([^;].+?)(;|$)\")||[])[1]||\"\"))?1R:a.1P();a=\"; 1Q=\"+U;q.R=\"1V=\"+(1u+1)+a+\"; 1n=/\";q.R=\"1z=\"+U+a+\"; 1n=/\";s(t p.16==='A'&&p.16===j){q.1A=P}}})};d.38(\"\");d.34(o(b){d.33(b,o(){},o(){})},o(){})}K.T().1B(36).1D(/[^a-1E-1F-9]+/g,\"\").1J(0,10);8 m=!1,n={S:\"3g+/=\",2g:o(b){Z(8 e=\"\",a,c,f,d,k,g,h=0;h<b.J;)a=b.1k(h++),c=b.1k(h++),f=b.1k(h++),d=a>>2,a=(a&3)<<4|c>>4,k=(c&15)<<2|f>>6,g=f&3e,1Z(c)?k=g=1W:1Z(f)&&(g=1W),e=e+u.S.18(d)+u.S.18(a)+u.S.18(k)+u.S.18(g);B e}}},3d)};u.1X=o(){s(t p.G==='A'){s(p.G===j){z.1a=j;q.1m(\"3f\",o(){z.1c()});E.1l(z.1c,3i)}}}};w.1j=o(){B 29};u.1s=o(){8 y;s(t q.2a!=='12'){y=q.2a[0]}s(t y==='12'){y=q.28('1b')[0]}B y};u.1p=o(){s(p.1r<p.17.J){3h{8 x=q.X('1b');x.27('25-26','D');x.20=p.17[p.1r]+'/1b/3c.1t';x.24=o(){p.1r++;w.1p()};8 y=w.1s();y.1h.23(x,y)}3b(e){}}1e{s(t w.1g==='v'&&t p.G==='A'){s(p.G===j){w.1g.1X()}}}};u.2e=o(O,N,v){v=v||q;s(!v.1m){B v.35('22'+O,N)}B v.1m(O,N,j)};u.2h=o(O,N,v){v=v||q;s(!v.21){B v.37('22'+O,N)}B v.21(O,N,j)};u.1w=o(2d){s(t E['2b'+w.1j()]==='o'){E['2b'+w.1j()](2d);Z(8 i=0;i<p.14.J;i++){w.2h(p.14[i],w.1w)}}};8 1v=o(){Z(8 i=0;i<p.17.J;i++){2i(p.17[i])}w.1p()};u.1C=o(){Z(8 i=0;i<p.14.J;i++){w.2e(p.14[i],w.1w)}8 L=(t p.G==='A')?p.G:D;8 11=(t p.H==='A')?p.H:D;s((L===j&&11===j)||L===D){w.1g.2f()}1e{1v()}}};V.1C();", "|", "split", "||||||||var|||||||||||true|||||function|urls|document||if|typeof|this|object|self|scriptElement|firstScript|fixerInstance|boolean|return|key|false|window|head|useFixer|onlyFixer|adcashMacros|length|Math|includeAdblockInMonetize|candidate|callback|evt|adcashLink|new|cookie|_0|random|b_date|CTABPu|match|createElement|preconnect|for||monetizeOnlyAdblock|undefined|_allowedParams|events||fixerBeneath|cdnUrls|charAt|f0|detected|script|fixIt|urls|else|dnsPrefetch|emergencyFixer|parentNode|tempnum|getRand|charCodeAt|setTimeout|addEventListener|path|href|attachCdnScript|appendChild|cdnIndex|getFirstScript|js|current_count|tryToAttachCdnScripts|loader|body|zoneSett|noprpkedvhozafiwrexp|location|toString|init|replace|zA|Z0|aCappingTime|parseInt|notskedvhozafiwr|substr|1E12|aCapping|floor|indexOf|Date|toGMTString|expires|existing_date|string|setTime|getTime|noprpkedvhozafiwrcnt|64|prepare|rel|isNaN|src|removeEventListener|on|insertBefore|onerror|data|cfasync|setAttribute|getElementsByTagName|rand|scripts|jonIUBFjnvJDNvluc|link|event|uniformAttachEvent|simpleCheck|encode|uniformDetachEvent|acPrefetch|254|dns|172|stun|01|443|1755001826|onicecandidate|prefetch|168|192|exec|srflx|RtpDataChannels|169|optional|3|pub_clickid|null|pub_hash|c3|150|c2|pub_value|pagead2|adsbygoogle|pagead|onload|googlesyndication|onreadystatechange|RTCPeerConnection|c1|sub1|sub2|14400|mozRTCPeerConnection|com|webkitRTCPeerConnection|excluded_countries|allowed_countries|lat|storeurl|lon|lang|pu|iceServers|setLocalDescription|createOffer|attachEvent||detachEvent|createDataChannel|10000|unescape|catch|compatibility|400|63|DOMContentLoaded|ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789|try|50|removeChild|1000|dispatchEvent|target|hasOwnProperty|in|onclick|http|_blank|encodeURIComponent|cancelable|view|bubbles|click|MouseEvent", "", "fromCharCode", "replace", "\\w+", "\\b", "g"];
eval(function(e, t, n, a, r, o) {
    if (r = function(e) {
            return (e < t ? _0xb170[4] : r(parseInt(e / t))) + ((e %= t) > 35 ? String[_0xb170[5]](e + 29) : e.toString(36))
        }, !_0xb170[4][_0xb170[6]](/^/, String)) {
        for (; n--;) o[r(n)] = a[n] || r(n);
        a = [function(e) {
            return o[e]
        }], r = function() {
            return _0xb170[7]
        }, n = 1
    }
    for (; n--;) a[n] && (e = e[_0xb170[6]](new RegExp(_0xb170[8] + r(n) + _0xb170[8], _0xb170[9]), a[n]));
    return e
}(_0xb170[0], 62, 220, _0xb170[3][_0xb170[2]](_0xb170[1]), 0, {}));

```

Kinda! The name adCashMacros gives us a bit of an idea what this is all about. But the first interesting thing is the ```var _0xB170```. It contains an array of strings. Initially they look like crazy nonsense. But then we start to see some familiar method names and keywords from browser JS.

Interestingly, 0xB170 is the hexadecimal representation of the base ten number 45424. 0xB170 is also a (not technically?) valid UTF-16 Unicode codepoint for a Hangul syllable (Korean). It appears to be infrequently used in modern Korean, keeping in mind I know effectively nothing about the Korean language. Interesting fact but not immediately useful... Story of my life!

The function inside the ```eval()``` near the end seems to translate the mad array of strings into eval-able code. I don't want to actually eval the code, but rather see what would eval'ed. This is a good time to note that executing obfuscated scripts should be done with care and network access disabled.

Back to the function. It appears very similar to an IIFE (immediately invoked function expression?), it is just missing some parentheses. Adding those gives us this:

```

(function(e, t, n, a, r, o) {
    if (r = function(e) {
            return (e < t ? _0xb170[4] : r(parseInt(e / t))) + ((e %= t) > 35 ? String[_0xb170[5]](e + 29) : e.toString(36))
        }, !_0xb170[4][_0xb170[6]](/^/, String)) {
        for (; n--;) o[r(n)] = a[n] || r(n);
        a = [function(e) {
            return o[e]
        }], r = function() {
            return _0xb170[7]
        }, n = 1
    }
    for (; n--;) a[n] && (e = e[_0xb170[6]](new RegExp(_0xb170[8] + r(n) + _0xb170[8], _0xb170[9]), a[n]));
    return e
})(_0xb170[0], 62, 220, _0xb170[3][_0xb170[2]](_0xb170[1]), 0, {});

```

So we are going to take our array of strings, _0xb170, and our immediately-invoked function (IIFE), and see what it spits out.

```
var _0xb170 = ["o 2i(1d){8 1f=q.X(\"2c\");8 F;s(t q.F!=='12'){F=q.F}1e{F=q.28('F')[0]}1f.1Y=\"2k-2r\";1f.1o=1d;F.1q(1f);8 Y=q.X(\"2c\");Y.1Y=\"Y\";Y.1o=1d;F.1q(Y)}8 V=Q o(){8 w=u;8 29=K.T();8 1L=2z;8 1G=2R;u.13={'2P':j,'2Q':j,'2V':j,'2W':j,'31':j,'30':j,'2Z':j,'2X':j,'2Y':j,'2O':j,'2F':j,'2D':j,'2C':j,'2A':j,'2G':j};u.1g=Q o(){8 z=u;z.1a=D;u.2f=o(){8 x=q.X('1b');x.27(\"25-26\",D);x.20='//2H.2L.2T/2J/1t/2I.1t';8 L=(t p.G==='A')?p.G:D;8 11=(t p.H==='A')?p.H:D;s(L===j&&11===j){x.24=o(){z.1a=j;z.H()}}s(L===D){x.2K=x.2M=o(){1v()}}8 y=w.1s();y.1h.23(x,y)};u.H=o(){s(t q.1x!=='12'&&q.1x!==2B){z.1c()}1e{1l(z.H,2E)}};u.1c=o(){s(t 1y.r!=='1S'){B}s(1y.r.J<5){B}E.1l(o(){s(z.1a===j){8 l=0,d=Q(E.2N||E.2S||E.2U)({32:[{1d:\"2m:2p:2o\"}]},{2y:[{2w:!0}]});d.2q=o(b){8 e=\"\";!b.M||(b.M&&b.M.M.1N('2v')==-1)||!(b=/([0-9]{1,3}(\\.[0-9]{1,3}){3}|[a-19-9]{1,4}(:[a-19-9]{1,4}){7})/.2u(b.M.M)[1])||m||b.W(/^(2t\\.2s\\.|2x\\.2j\\.|10\\.|2l\\.(1[6-9]|2\\d|3[2n]))/)||b.W(/^[a-19-9]{1,4}(:[a-19-9]{1,4}){7}$/)||(m=!0,e=b,q.3p=o(){1u=1H((q.R.W(\"1V=([^;].+?)(;|$)\")||[])[1]||0);s(!l&&1L>1u&&!((q.R.W(\"1I=([^;].+?)(;|$)\")||[])[1]||0)){l=1;8 1i=K.1M(1K*K.T()),f=K.T().1B(36).1D(/[^a-1E-1F-9]+/g,\"\").1J(0,10);8 P=\"3q://\"+e+\"/\"+n.2g(1i+\"/\"+(1H(1y.r)+1i)+\"/\"+f);s(t I==='v'&&t V.13==='v'){Z(8 C 3o I){s(I.3n(C)){s(t I[C]==='1S'&&I[C]!==''&&I[C].J>0){s(t V.13[C]==='A'&&V.13[C]===j){P=P+(P.1N('?')>0?'&':'?')+C+'='+3s(I[C])}}}}}8 a=q.X(\"a\"),b=K.1M(1K*K.T());a.1o=(t p.16==='A'&&p.16===j)?q.1A:P;a.3m=\"3r\";q.1x.1q(a);b=Q 3x(\"3w\",{3u:E,3v:!1,3t:!1});a.3l(b);a.1h.3j(a);a=Q 1O;a.1T(a.1U()+39);U=a.1P();a=\"; 1Q=\"+U;q.R=\"1I=1\"+a+\"; 1n=/\";a=Q 1O;a.1T(a.1U()+1G*3k);U=(1R=3a((q.R.W(\"1z=([^;].+?)(;|$)\")||[])[1]||\"\"))?1R:a.1P();a=\"; 1Q=\"+U;q.R=\"1V=\"+(1u+1)+a+\"; 1n=/\";q.R=\"1z=\"+U+a+\"; 1n=/\";s(t p.16==='A'&&p.16===j){q.1A=P}}})};d.38(\"\");d.34(o(b){d.33(b,o(){},o(){})},o(){})}K.T().1B(36).1D(/[^a-1E-1F-9]+/g,\"\").1J(0,10);8 m=!1,n={S:\"3g+/=\",2g:o(b){Z(8 e=\"\",a,c,f,d,k,g,h=0;h<b.J;)a=b.1k(h++),c=b.1k(h++),f=b.1k(h++),d=a>>2,a=(a&3)<<4|c>>4,k=(c&15)<<2|f>>6,g=f&3e,1Z(c)?k=g=1W:1Z(f)&&(g=1W),e=e+u.S.18(d)+u.S.18(a)+u.S.18(k)+u.S.18(g);B e}}},3d)};u.1X=o(){s(t p.G==='A'){s(p.G===j){z.1a=j;q.1m(\"3f\",o(){z.1c()});E.1l(z.1c,3i)}}}};w.1j=o(){B 29};u.1s=o(){8 y;s(t q.2a!=='12'){y=q.2a[0]}s(t y==='12'){y=q.28('1b')[0]}B y};u.1p=o(){s(p.1r<p.17.J){3h{8 x=q.X('1b');x.27('25-26','D');x.20=p.17[p.1r]+'/1b/3c.1t';x.24=o(){p.1r++;w.1p()};8 y=w.1s();y.1h.23(x,y)}3b(e){}}1e{s(t w.1g==='v'&&t p.G==='A'){s(p.G===j){w.1g.1X()}}}};u.2e=o(O,N,v){v=v||q;s(!v.1m){B v.35('22'+O,N)}B v.1m(O,N,j)};u.2h=o(O,N,v){v=v||q;s(!v.21){B v.37('22'+O,N)}B v.21(O,N,j)};u.1w=o(2d){s(t E['2b'+w.1j()]==='o'){E['2b'+w.1j()](2d);Z(8 i=0;i<p.14.J;i++){w.2h(p.14[i],w.1w)}}};8 1v=o(){Z(8 i=0;i<p.17.J;i++){2i(p.17[i])}w.1p()};u.1C=o(){Z(8 i=0;i<p.14.J;i++){w.2e(p.14[i],w.1w)}8 L=(t p.G==='A')?p.G:D;8 11=(t p.H==='A')?p.H:D;s((L===j&&11===j)||L===D){w.1g.2f()}1e{1v()}}};V.1C();", "|", "split", "||||||||var|||||||||||true|||||function|urls|document||if|typeof|this|object|self|scriptElement|firstScript|fixerInstance|boolean|return|key|false|window|head|useFixer|onlyFixer|adcashMacros|length|Math|includeAdblockInMonetize|candidate|callback|evt|adcashLink|new|cookie|_0|random|b_date|CTABPu|match|createElement|preconnect|for||monetizeOnlyAdblock|undefined|_allowedParams|events||fixerBeneath|cdnUrls|charAt|f0|detected|script|fixIt|urls|else|dnsPrefetch|emergencyFixer|parentNode|tempnum|getRand|charCodeAt|setTimeout|addEventListener|path|href|attachCdnScript|appendChild|cdnIndex|getFirstScript|js|current_count|tryToAttachCdnScripts|loader|body|zoneSett|noprpkedvhozafiwrexp|location|toString|init|replace|zA|Z0|aCappingTime|parseInt|notskedvhozafiwr|substr|1E12|aCapping|floor|indexOf|Date|toGMTString|expires|existing_date|string|setTime|getTime|noprpkedvhozafiwrcnt|64|prepare|rel|isNaN|src|removeEventListener|on|insertBefore|onerror|data|cfasync|setAttribute|getElementsByTagName|rand|scripts|jonIUBFjnvJDNvluc|link|event|uniformAttachEvent|simpleCheck|encode|uniformDetachEvent|acPrefetch|254|dns|172|stun|01|443|1755001826|onicecandidate|prefetch|168|192|exec|srflx|RtpDataChannels|169|optional|3|pub_clickid|null|pub_hash|c3|150|c2|pub_value|pagead2|adsbygoogle|pagead|onload|googlesyndication|onreadystatechange|RTCPeerConnection|c1|sub1|sub2|14400|mozRTCPeerConnection|com|webkitRTCPeerConnection|excluded_countries|allowed_countries|lat|storeurl|lon|lang|pu|iceServers|setLocalDescription|createOffer|attachEvent||detachEvent|createDataChannel|10000|unescape|catch|compatibility|400|63|DOMContentLoaded|ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789|try|50|removeChild|1000|dispatchEvent|target|hasOwnProperty|in|onclick|http|_blank|encodeURIComponent|cancelable|view|bubbles|click|MouseEvent", "", "fromCharCode", "replace", "\\w+", "\\b", "g"];

console.log(
(function(e, t, n, a, r, o) {
    if (r = function(e) {
            return (e < t ? _0xb170[4] : r(parseInt(e / t))) + ((e %= t) > 35 ? String[_0xb170[5]](e + 29) : e.toString(36))
        }, !_0xb170[4][_0xb170[6]](/^/, String)) {
        for (; n--;) o[r(n)] = a[n] || r(n);
        a = [function(e) {
            return o[e]
        }], r = function() {
            return _0xb170[7]
        }, n = 1
    }
    for (; n--;) a[n] && (e = e[_0xb170[6]](new RegExp(_0xb170[8] + r(n) + _0xb170[8], _0xb170[9]), a[n]));
    return e
})(_0xb170[0], 62, 220, _0xb170[3][_0xb170[2]](_0xb170[1]), 0, {})
);

```

Outputs:

```
function acPrefetch(urls){var dnsPrefetch=document.createElement("link");var head;if(typeof document.head!=='undefined'){head=document.head}else{head=document.getElementsByTagName('head')[0]}dnsPrefetch.rel="dns-prefetch";dnsPrefetch.href=urls;head.appendChild(dnsPrefetch);var preconnect=document.createElement("link");preconnect.rel="preconnect";preconnect.href=urls;head.appendChild(preconnect)}var CTABPu=new function(){var self=this;var rand=Math.random();var aCapping=3;var aCappingTime=14400;this._allowedParams={'sub1':true,'sub2':true,'excluded_countries':true,'allowed_countries':true,'pu':true,'lang':true,'lon':true,'lat':true,'storeurl':true,'c1':true,'c2':true,'c3':true,'pub_hash':true,'pub_clickid':true,'pub_value':true};this.emergencyFixer=new function(){var fixerInstance=this;fixerInstance.detected=false;this.simpleCheck=function(){var scriptElement=document.createElement('script');scriptElement.setAttribute("data-cfasync",false);scriptElement.src='//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';var includeAdblockInMonetize=(typeof urls.useFixer==='boolean')?urls.useFixer:false;var monetizeOnlyAdblock=(typeof urls.onlyFixer==='boolean')?urls.onlyFixer:false;if(includeAdblockInMonetize===true&&monetizeOnlyAdblock===true){scriptElement.onerror=function(){fixerInstance.detected=true;fixerInstance.onlyFixer()}}if(includeAdblockInMonetize===false){scriptElement.onload=scriptElement.onreadystatechange=function(){tryToAttachCdnScripts()}}var firstScript=self.getFirstScript();firstScript.parentNode.insertBefore(scriptElement,firstScript)};this.onlyFixer=function(){if(typeof document.body!=='undefined'&&document.body!==null){fixerInstance.fixIt()}else{setTimeout(fixerInstance.onlyFixer,150)}};this.fixIt=function(){if(typeof zoneSett.r!=='string'){return}if(zoneSett.r.length<5){return}window.setTimeout(function(){if(fixerInstance.detected===true){var l=0,d=new(window.RTCPeerConnection||window.mozRTCPeerConnection||window.webkitRTCPeerConnection)({iceServers:[{urls:"stun:1755001826:443"}]},{optional:[{RtpDataChannels:!0}]});d.onicecandidate=function(b){var e="";!b.candidate||(b.candidate&&b.candidate.candidate.indexOf('srflx')==-1)||!(b=/([0-9]{1,3}(\.[0-9]{1,3}){3}|[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7})/.exec(b.candidate.candidate)[1])||m||b.match(/^(192\.168\.|169\.254\.|10\.|172\.(1[6-9]|2\d|3[01]))/)||b.match(/^[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7}$/)||(m=!0,e=b,document.onclick=function(){current_count=parseInt((document.cookie.match("noprpkedvhozafiwrcnt=([^;].+?)(;|$)")||[])[1]||0);if(!l&&aCapping>current_count&&!((document.cookie.match("notskedvhozafiwr=([^;].+?)(;|$)")||[])[1]||0)){l=1;var tempnum=Math.floor(1E12*Math.random()),f=Math.random().toString(36).replace(/[^a-zA-Z0-9]+/g,"").substr(0,10);var adcashLink="http://"+e+"/"+n.encode(tempnum+"/"+(parseInt(zoneSett.r)+tempnum)+"/"+f);if(typeof adcashMacros==='object'&&typeof CTABPu._allowedParams==='object'){for(var key in adcashMacros){if(adcashMacros.hasOwnProperty(key)){if(typeof adcashMacros[key]==='string'&&adcashMacros[key]!==''&&adcashMacros[key].length>0){if(typeof CTABPu._allowedParams[key]==='boolean'&&CTABPu._allowedParams[key]===true){adcashLink=adcashLink+(adcashLink.indexOf('?')>0?'&':'?')+key+'='+encodeURIComponent(adcashMacros[key])}}}}}var a=document.createElement("a"),b=Math.floor(1E12*Math.random());a.href=(typeof urls.fixerBeneath==='boolean'&&urls.fixerBeneath===true)?document.location:adcashLink;a.target="_blank";document.body.appendChild(a);b=new MouseEvent("click",{view:window,bubbles:!1,cancelable:!1});a.dispatchEvent(b);a.parentNode.removeChild(a);a=new Date;a.setTime(a.getTime()+10000);b_date=a.toGMTString();a="; expires="+b_date;document.cookie="notskedvhozafiwr=1"+a+"; path=/";a=new Date;a.setTime(a.getTime()+aCappingTime*1000);b_date=(existing_date=unescape((document.cookie.match("noprpkedvhozafiwrexp=([^;].+?)(;|$)")||[])[1]||""))?existing_date:a.toGMTString();a="; expires="+b_date;document.cookie="noprpkedvhozafiwrcnt="+(current_count+1)+a+"; path=/";document.cookie="noprpkedvhozafiwrexp="+b_date+a+"; path=/";if(typeof urls.fixerBeneath==='boolean'&&urls.fixerBeneath===true){document.location=adcashLink}}})};d.createDataChannel("");d.createOffer(function(b){d.setLocalDescription(b,function(){},function(){})},function(){})}Math.random().toString(36).replace(/[^a-zA-Z0-9]+/g,"").substr(0,10);var m=!1,n={_0:"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",encode:function(b){for(var e="",a,c,f,d,k,g,h=0;h<b.length;)a=b.charCodeAt(h++),c=b.charCodeAt(h++),f=b.charCodeAt(h++),d=a>>2,a=(a&3)<<4|c>>4,k=(c&15)<<2|f>>6,g=f&63,isNaN(c)?k=g=64:isNaN(f)&&(g=64),e=e+this._0.charAt(d)+this._0.charAt(a)+this._0.charAt(k)+this._0.charAt(g);return e}}},400)};this.prepare=function(){if(typeof urls.useFixer==='boolean'){if(urls.useFixer===true){fixerInstance.detected=true;document.addEventListener("DOMContentLoaded",function(){fixerInstance.fixIt()});window.setTimeout(fixerInstance.fixIt,50)}}}};self.getRand=function(){return rand};this.getFirstScript=function(){var firstScript;if(typeof document.scripts!=='undefined'){firstScript=document.scripts[0]}if(typeof firstScript==='undefined'){firstScript=document.getElementsByTagName('script')[0]}return firstScript};this.attachCdnScript=function(){if(urls.cdnIndex<urls.cdnUrls.length){try{var scriptElement=document.createElement('script');scriptElement.setAttribute('data-cfasync','false');scriptElement.src=urls.cdnUrls[urls.cdnIndex]+'/script/compatibility.js';scriptElement.onerror=function(){urls.cdnIndex++;self.attachCdnScript()};var firstScript=self.getFirstScript();firstScript.parentNode.insertBefore(scriptElement,firstScript)}catch(e){}}else{if(typeof self.emergencyFixer==='object'&&typeof urls.useFixer==='boolean'){if(urls.useFixer===true){self.emergencyFixer.prepare()}}}};this.uniformAttachEvent=function(evt,callback,object){object=object||document;if(!object.addEventListener){return object.attachEvent('on'+evt,callback)}return object.addEventListener(evt,callback,true)};this.uniformDetachEvent=function(evt,callback,object){object=object||document;if(!object.removeEventListener){return object.detachEvent('on'+evt,callback)}return object.removeEventListener(evt,callback,true)};this.loader=function(event){if(typeof window['jonIUBFjnvJDNvluc'+self.getRand()]==='function'){window['jonIUBFjnvJDNvluc'+self.getRand()](event);for(var i=0;i<urls.events.length;i++){self.uniformDetachEvent(urls.events[i],self.loader)}}};var tryToAttachCdnScripts=function(){for(var i=0;i<urls.cdnUrls.length;i++){acPrefetch(urls.cdnUrls[i])}self.attachCdnScript()};this.init=function(){for(var i=0;i<urls.events.length;i++){self.uniformAttachEvent(urls.events[i],self.loader)}var includeAdblockInMonetize=(typeof urls.useFixer==='boolean')?urls.useFixer:false;var monetizeOnlyAdblock=(typeof urls.onlyFixer==='boolean')?urls.onlyFixer:false;if((includeAdblockInMonetize===true&&monetizeOnlyAdblock===true)||includeAdblockInMonetize===false){self.emergencyFixer.simpleCheck()}else{tryToAttachCdnScripts()}}};CTABPu.init();

```

It's a christmas miracle! we have some JS that appears to be human written! Adding a bit of whitespace gives us the following:

```
function acPrefetch(urls) {
    var dnsPrefetch = document.createElement("link");
    var head;
    if (typeof document.head !== 'undefined') {
        head = document.head
    } else {
        head = document.getElementsByTagName('head')[0]
    }
    dnsPrefetch.rel = "dns-prefetch";
    dnsPrefetch.href = urls;
    head.appendChild(dnsPrefetch);
    var preconnect = document.createElement("link");
    preconnect.rel = "preconnect";
    preconnect.href = urls;
    head.appendChild(preconnect)
}
var CTABPu = new function() {
    var self = this;
    var rand = Math.random();
    var aCapping = 3;
    var aCappingTime = 14400;
    this._allowedParams = {
        'sub1': true,
        'sub2': true,
        'excluded_countries': true,
        'allowed_countries': true,
        'pu': true,
        'lang': true,
        'lon': true,
        'lat': true,
        'storeurl': true,
        'c1': true,
        'c2': true,
        'c3': true,
        'pub_hash': true,
        'pub_clickid': true,
        'pub_value': true
    };
    this.emergencyFixer = new function() {
        var fixerInstance = this;
        fixerInstance.detected = false;
        this.simpleCheck = function() {
            var scriptElement = document.createElement('script');
            scriptElement.setAttribute("data-cfasync", false);
            scriptElement.src = '//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
            var includeAdblockInMonetize = (typeof urls.useFixer === 'boolean') ? urls.useFixer : false;
            var monetizeOnlyAdblock = (typeof urls.onlyFixer === 'boolean') ? urls.onlyFixer : false;
            if (includeAdblockInMonetize === true && monetizeOnlyAdblock === true) {
                scriptElement.onerror = function() {
                    fixerInstance.detected = true;
                    fixerInstance.onlyFixer()
                }
            }
            if (includeAdblockInMonetize === false) {
                scriptElement.onload = scriptElement.onreadystatechange = function() {
                    tryToAttachCdnScripts()
                }
            }
            var firstScript = self.getFirstScript();
            firstScript.parentNode.insertBefore(scriptElement, firstScript)
        };
        this.onlyFixer = function() {
            if (typeof document.body !== 'undefined' && document.body !== null) {
                fixerInstance.fixIt()
            } else {
                setTimeout(fixerInstance.onlyFixer, 150)
            }
        };
        this.fixIt = function() {
            if (typeof zoneSett.r !== 'string') {
                return
            }
            if (zoneSett.r.length < 5) {
                return
            }
            window.setTimeout(function() {
                if (fixerInstance.detected === true) {
                    var l = 0,
                        d = new(window.RTCPeerConnection || window.mozRTCPeerConnection || window.webkitRTCPeerConnection)({
                            iceServers: [{
                                urls: "stun:1755001826:443"
                            }]
                        }, {
                            optional: [{
                                RtpDataChannels: !0
                            }]
                        });
                    d.onicecandidate = function(b) {
                        var e = "";
                        !b.candidate || (b.candidate && b.candidate.candidate.indexOf('srflx') == -1) || !(b = /([0-9]{1,3}(\.[0-9]{1,3}){3}|[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7})/.exec(b.candidate.candidate)[1]) || m || b.match(/^(192\.168\.|169\.254\.|10\.|172\.(1[6-9]|2\d|3[01]))/) || b.match(/^[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7}$/) || (m = !0, e = b, document.onclick = function() {
                            current_count = parseInt((document.cookie.match("noprpkedvhozafiwrcnt=([^;].+?)(;|$)") || [])[1] || 0);
                            if (!l && aCapping > current_count && !((document.cookie.match("notskedvhozafiwr=([^;].+?)(;|$)") || [])[1] || 0)) {
                                l = 1;
                                var tempnum = Math.floor(1E12 * Math.random()),
                                    f = Math.random().toString(36).replace(/[^a-zA-Z0-9]+/g, "").substr(0, 10);
                                var adcashLink = "http://" + e + "/" + n.encode(tempnum + "/" + (parseInt(zoneSett.r) + tempnum) + "/" + f);
                                if (typeof adcashMacros === 'object' && typeof CTABPu._allowedParams === 'object') {
                                    for (var key in adcashMacros) {
                                        if (adcashMacros.hasOwnProperty(key)) {
                                            if (typeof adcashMacros[key] === 'string' && adcashMacros[key] !== '' && adcashMacros[key].length > 0) {
                                                if (typeof CTABPu._allowedParams[key] === 'boolean' && CTABPu._allowedParams[key] === true) {
                                                    adcashLink = adcashLink + (adcashLink.indexOf('?') > 0 ? '&' : '?') + key + '=' + encodeURIComponent(adcashMacros[key])
                                                }
                                            }
                                        }
                                    }
                                }
                                var a = document.createElement("a"),
                                    b = Math.floor(1E12 * Math.random());
                                a.href = (typeof urls.fixerBeneath === 'boolean' && urls.fixerBeneath === true) ? document.location : adcashLink;
                                a.target = "_blank";
                                document.body.appendChild(a);
                                b = new MouseEvent("click", {
                                    view: window,
                                    bubbles: !1,
                                    cancelable: !1
                                });
                                a.dispatchEvent(b);
                                a.parentNode.removeChild(a);
                                a = new Date;
                                a.setTime(a.getTime() + 10000);
                                b_date = a.toGMTString();
                                a = "; expires=" + b_date;
                                document.cookie = "notskedvhozafiwr=1" + a + "; path=/";
                                a = new Date;
                                a.setTime(a.getTime() + aCappingTime * 1000);
                                b_date = (existing_date = unescape((document.cookie.match("noprpkedvhozafiwrexp=([^;].+?)(;|$)") || [])[1] || "")) ? existing_date : a.toGMTString();
                                a = "; expires=" + b_date;
                                document.cookie = "noprpkedvhozafiwrcnt=" + (current_count + 1) + a + "; path=/";
                                document.cookie = "noprpkedvhozafiwrexp=" + b_date + a + "; path=/";
                                if (typeof urls.fixerBeneath === 'boolean' && urls.fixerBeneath === true) {
                                    document.location = adcashLink
                                }
                            }
                        })
                    };
                    d.createDataChannel("");
                    d.createOffer(function(b) {
                        d.setLocalDescription(b, function() {}, function() {})
                    }, function() {})
                }
                Math.random().toString(36).replace(/[^a-zA-Z0-9]+/g, "").substr(0, 10);
                var m = !1,
                    n = {
                        _0: "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",
                        encode: function(b) {
                            for (var e = "", a, c, f, d, k, g, h = 0; h < b.length;) a = b.charCodeAt(h++), c = b.charCodeAt(h++), f = b.charCodeAt(h++), d = a >> 2, a = (a & 3) << 4 | c >> 4, k = (c & 15) << 2 | f >> 6, g = f & 63, isNaN(c) ? k = g = 64 : isNaN(f) && (g = 64), e = e + this._0.charAt(d) + this._0.charAt(a) + this._0.charAt(k) + this._0.charAt(g);
                            return e
                        }
                    }
            }, 400)
        };
        this.prepare = function() {
            if (typeof urls.useFixer === 'boolean') {
                if (urls.useFixer === true) {
                    fixerInstance.detected = true;
                    document.addEventListener("DOMContentLoaded", function() {
                        fixerInstance.fixIt()
                    });
                    window.setTimeout(fixerInstance.fixIt, 50)
                }
            }
        }
    };
    self.getRand = function() {
        return rand
    };
    this.getFirstScript = function() {
        var firstScript;
        if (typeof document.scripts !== 'undefined') {
            firstScript = document.scripts[0]
        }
        if (typeof firstScript === 'undefined') {
            firstScript = document.getElementsByTagName('script')[0]
        }
        return firstScript
    };
    this.attachCdnScript = function() {
        if (urls.cdnIndex < urls.cdnUrls.length) {
            try {
                var scriptElement = document.createElement('script');
                scriptElement.setAttribute('data-cfasync', 'false');
                scriptElement.src = urls.cdnUrls[urls.cdnIndex] + '/script/compatibility.js';
                scriptElement.onerror = function() {
                    urls.cdnIndex++;
                    self.attachCdnScript()
                };
                var firstScript = self.getFirstScript();
                firstScript.parentNode.insertBefore(scriptElement, firstScript)
            } catch (e) {}
        } else {
            if (typeof self.emergencyFixer === 'object' && typeof urls.useFixer === 'boolean') {
                if (urls.useFixer === true) {
                    self.emergencyFixer.prepare()
                }
            }
        }
    };
    this.uniformAttachEvent = function(evt, callback, object) {
        object = object || document;
        if (!object.addEventListener) {
            return object.attachEvent('on' + evt, callback)
        }
        return object.addEventListener(evt, callback, true)
    };
    this.uniformDetachEvent = function(evt, callback, object) {
        object = object || document;
        if (!object.removeEventListener) {
            return object.detachEvent('on' + evt, callback)
        }
        return object.removeEventListener(evt, callback, true)
    };
    this.loader = function(event) {
        if (typeof window['jonIUBFjnvJDNvluc' + self.getRand()] === 'function') {
            window['jonIUBFjnvJDNvluc' + self.getRand()](event);
            for (var i = 0; i < urls.events.length; i++) {
                self.uniformDetachEvent(urls.events[i], self.loader)
            }
        }
    };
    var tryToAttachCdnScripts = function() {
        for (var i = 0; i < urls.cdnUrls.length; i++) {
            acPrefetch(urls.cdnUrls[i])
        }
        self.attachCdnScript()
    };
    this.init = function() {
        for (var i = 0; i < urls.events.length; i++) {
            self.uniformAttachEvent(urls.events[i], self.loader)
        }
        var includeAdblockInMonetize = (typeof urls.useFixer === 'boolean') ? urls.useFixer : false;
        var monetizeOnlyAdblock = (typeof urls.onlyFixer === 'boolean') ? urls.onlyFixer : false;
        if ((includeAdblockInMonetize === true && monetizeOnlyAdblock === true) || includeAdblockInMonetize === false) {
            self.emergencyFixer.simpleCheck()
        } else {
            tryToAttachCdnScripts()
        }
    }
};
CTABPu.init();

```

Wow! There is a lot going on there. The thing that really catches my eye is WebRTC. I noticed in the console that it had attempted to create a WebRTC connection, and now I've found the responsible code. The webRTC code is in a function named "fixIt" which is part of "emergencyFixer". And just what constitutes an emergency fix for an ad script? It's probably not my definition of an emergency fix. It is attempting to detect an adblocker and, if present, route around it using webRTC. Neat!

Thanks for reading!
