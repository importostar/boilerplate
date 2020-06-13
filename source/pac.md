---
title: pac
date: 2020-05-07
---
Example Python program pac.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import ipaddress
* import socket
* import fnmatch
* import traceback
* import itertools
* from datetime import datetime
* import functools
* from urllib.parse import urlparse
* from PyQt5.QtCore import QObject, QVariant, QMetaType, pyqtSlot
* from PyQt5.QtQml import QJSEngine, QJSValue
* from PyQt5.QtNetwork import QNetworkProxy

## Classes

* class ParseProxyError(Exception):
* class EvalProxyError(Exception):
* class _PACContext(QObject):
* class PACResolver(object):

## Methods

*   def _js_slot(*args):
* def decorator(method):
*   def new_method(self, *args, **kwargs):
*   def __init__(self, engine):
*   def isPlainHostName(self, host):
*   def dnsDomainIs(self, host, domain):
*   def localHostOrDomainIs(self, host, hostdom):
*   def isResolvable(self, host):
*   def isInNet(self, host, pattern, mask):
*   def dnsResolve(self, host):
*   def myIpAddress(self):
*   def dnsDomainLevels(self, host):
*   def shExpMatch(self, str, shexp):
*   def weekdayRange(self, args):
*   def dateRange(self, args):
*   def timeRange(self, args):
*   def _parse_proxy_entry(proxy_str):
*   def _parse_proxy_string(proxy_str):
*   def __init__(self, pac_str):
*   def resolve(self, url_str):

## Code

Example Python PyQt program :

    import sys
    import ipaddress
    import socket
    import fnmatch
    import traceback
    import itertools
    from datetime import datetime
    import functools
    from urllib.parse import urlparse
    from PyQt5.QtCore import QObject, QVariant, QMetaType, pyqtSlot
    from PyQt5.QtQml import QJSEngine, QJSValue
    from PyQt5.QtNetwork import QNetworkProxy
      
    class ParseProxyError(Exception):
      pass
      
    class EvalProxyError(Exception):
      pass
    
    class _PACContext(QObject):
      def _js_slot(*args):
        def decorator(method):
          @functools.wraps(method)
          def new_method(self, *args, **kwargs):
            try:
              return method(self, *args, **kwargs)
            except:
              traceback.print_exc()
              e = sys.exc_info()[0]
              return self._error_con.callAsConstructor([str(e)])
          return pyqtSlot(*args, result=QJSValue)(new_method)
        return decorator
    
      def __init__(self, engine):
        QObject.__init__(self)
        self._engine = engine
        self._error_con = engine.globalObject().property("Error")
      
      @_js_slot(str)
      def isPlainHostName(self, host):
        return '.' not in host
        
      @_js_slot(str, str)
      def dnsDomainIs(self, host, domain):
        return host.endswith(domain)
      
      @_js_slot(str, str)
      def localHostOrDomainIs(self, host, hostdom):
        (_, dot_host, _) = host.partition('.')
        (unqual_hostdom, _, _) = hostdom.partition('.')
        if dot_host == "":
          return host == unqual_hostdom
        else:
          return host == hostdom
      
      @_js_slot(str)
      def isResolvable(self, host):
        return self.dnsResolve(host) != ""
      
      @_js_slot(str, str, str)
      def isInNet(self, host, pattern, mask):
        host_ip = ipaddress.ip_address(host)
        network = ipaddress.ip_network("{}/{}".format(pattern, mask))
        return host_ip in network
      
      @_js_slot(str)
      def dnsResolve(self, host):
        try:
          return socket.getaddrinfo(host, None)[0][4][0]
        except socket.gaierror:
          return ""
    
      @_js_slot()
      def myIpAddress(self):
        return socket.gethostbyname(socket.gethostname())
    
      @_js_slot(str)
      def dnsDomainLevels(self, host):
        return host.count('.')
      
      @_js_slot(str, str)
      def shExpMatch(self, str, shexp):
        return fnmatch.fnmatchcase(str, shexp)
      
      @_js_slot(QVariant)
      def weekdayRange(self, args):
        args = args.toVariant()
        wd1 = args[0]
        wd2 = wd1
        gmt = args[-1] == "GMT"
        if gmt:
          args = args[:-1]
    
        if len(args) == 2:
          wd2 = args[1]
        elif len(args) != 1:
          raise EvalProxyError("Invalid number of arguments")
    
        weekdays = ["MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"]
        curtime = datetime.utcnow() if gmt else datetime.now()
        return weekdays.index(wd1) <= curtime.weekday() <= weekdays.index(wd2)
      
      @_js_slot(QVariant)
      def dateRange(self, args):
        args = args.toVariant()
        order = ["day", "month", "year"]
        args1 = {}
        args2 = {}
        gmt = args[-1] == "GMT"
        if gmt:
          args = args[:-1]
    
        my_order = []
        count = 0
        for arg in args:
          argtype = "year"
          if type(arg) is str:
            argtype = "month"
          elif arg >= 1 and arg <= 31:
            argtype = "day"
    
          if argtype in args1:
            break
          if any(map(lambda x: x in args1, order[order.index(argtype) + 1:])):
            raise EvalProxyError("Invalid arguments order")
    
          args1[argtype] = arg
          my_order.append(argtype)
          count += 1
    
        if len(args) == 2 * count:
          for e, i in zip(my_order, itertools.count(0)):
            args2[e] = args[count + i]
        elif len(args) == count:
          args2 = args1
        else:
          raise EvalProxyError("Invalid number of arguments")
    
        if len(args1) == 0:
          raise EvalProxyError("Nothing is passed to check the range")
        months = ["JAN", "FEB", "MAR", "APR", "MAY", "JUN", "JUL", "AUG", "SEP", "OCT", "NOV", "DEC"];
        curtime = datetime.utcnow() if gmt else datetime.now()
        if "day" in args1 and not (args1["day"] <= curtime.day <= args2["day"]):
          return False
        if "month" in args1 and not (months.index(args1["month"]) <= curtime.month - 1 <= months.index(args2["month"])):
          return False
        if "year" in args1 and not (args1["year"] <= curtime.year <= args2["year"]):
          return False
        return True
      
      @_js_slot(QVariant)
      def timeRange(self, args):
        args = args.toVariant()
        args1 = {}
        args2 = {}
        gmt = args[-1] == "GMT"
        if gmt:
          args = args[:-1]
    
        if len(args) == 1:
          args1["hour"] = args[0]
          args2["hour"] = args[0] + 1
        else:
          order = ["hour", "min", "sec"]
          if len(args) % 2 != 0 or len(args) > len(order) * 2:
            raise EvalProxyError("Invalid number of arguments")
    
          for e, i in zip(order[:len(args) / 2], itertools.count(0)):
            args1[e] = args[i]
            args2[e] = args[len(arguments) / 2 + i]
    
        if len(args1) == 0:
          raise EvalProxyError("Nothing is passed to check the range")
        curtime = datetime.utcnow() if gmt else datetime.now()
        if "hour" in args1 and not (args1["hour"] <= curtime.hour < args2["hour"]):
          return False
        if "min" in args1 and not (args1["min"] <= curtime.minute < args2["min"]):
          return False
        if "sec" in args1 and not (args1["sec"] <= curtime.second < args2["sec"]):
          return False
        return True
    
    class PACResolver(object):
      @staticmethod
      def _parse_proxy_entry(proxy_str):
        config = list(filter(lambda s: s != "", proxy_str.split(' ')))
        if len(config) == 0:
          raise ParseProxyError("Empty proxy entry")
        try:
          if config[0] == "DIRECT":
            if len(config) != 1:
              raise ParseProxyError("Invalid number of parameters for DIRECT")
            return QNetworkProxy(QNetworkProxy.NoProxy)
          elif config[0] == "PROXY":
            if len(config) != 2:
              raise ParseProxyError("Invalid number of parameters for PROXY")
            host, _, port = config[1].partition(':')
            return QNetworkProxy(QNetworkProxy.HttpProxy, host, int(port))
          elif config[0] == "SOCKS":
            if len(config) != 2:
              raise ParseProxyError("Invalid number of parameters for SOCKS")
            host, _, port = config[1].partition(':')
            return QNetworkProxy(QNetworkProxy.Socks5Proxy, host, int(port))
          else:
            raise ParseProxyError("Unknown proxy type: {}".format(config[0]))
        except ValueError:
          raise ParseProxyError("Invalid port number")
    
      @staticmethod
      def _parse_proxy_string(proxy_str):
        return map(PACResolver._parse_proxy_entry, proxy_str.split(';'))
      
      def __init__(self, pac_str):
        self._engine = QJSEngine()
    
        self._engine.installExtensions(QJSEngine.ConsoleExtension)
        self._ctx = _PACContext(self._engine)
        self._engine.globalObject().setProperty("PAC", self._engine.newQObject(self._ctx))
        proxy_config = self._engine.newObject()
        proxy_config.setProperty("bindings", self._engine.newObject())
        self._engine.globalObject().setProperty("ProxyConfig", proxy_config)
        ctx_meta = self._ctx.metaObject()
        for i in range(ctx_meta.methodCount()):
          m = ctx_meta.method(i)
          if m.typeName() == "QJSValue":
            call_str = None
            if m.parameterCount() == 1 and m.parameterType(0) == QMetaType.QVariant:
              call_str = "PAC.{0}([].slice.call(arguments))"
            else:
              call_str = "PAC.{0}.apply(PAC, arguments)"
            decl_str = '''
              function {0}() {{
                var res = ''' + call_str + ''';
                if (res instanceof Error) {{
                  throw res;
                }} else {{
                  return res;
                }}
              }}
            '''
            self._engine.evaluate(decl_str.format(bytes(m.name()).decode()))
    
        self._engine.evaluate(pac_str, "pac")
        self._resolver = self._engine.globalObject().property("FindProxyForURL");
        if not self._resolver.isCallable():
          raise EvalProxyError("Cannot resolve FindProxyForURL function, got '{}' instead".format(self._resolver.toString()))
    
      def resolve(self, url_str):
        url = urlparse(url_str)
        domain, sep, port = url.netloc.rpartition(':')
        if sep == "":
          domain = port
        result = self._resolver.call([url_str, domain])
        result_str = result.toString()
        if not result.isString():
          raise EvalProxyError("Got strange value from FindProxyForURL: {}".format(result_str))
        return PACResolver._parse_proxy_string(result_str)
    
    TEST_PAC = '''
      function test(function_name, expect) {
        var args = Array.prototype.slice.call(arguments, 2);
        var fun_call = function_name + "(" + args.join(", ") + ")";
        console.log("Trying to test that " + fun_call + " === " + expect);
        var res = eval(function_name).apply(null, args);
        if(res !== expect) {
          throw new Error("failed test: " + fun_call + ": '" + res + "' !== '" + expect + "'");
        }
      }
    
      function proxyBindings() {
        return JSON.stringify(ProxyConfig.bindings);
      }
    
      function FindProxyForURL(domain, host) {
        test("isPlainHostName", true, "www");
        test("isPlainHostName", false, "www.netscape.com");
    
        test("dnsDomainIs", true, "www.netscape.com", ".netscape.com");
        test("dnsDomainIs", false, "www", ".netscape.com");
        test("dnsDomainIs", false, "www.mcom.com", ".netscape.com");
    
        test("localHostOrDomainIs", true, "www.netscape.com", "www.netscape.com");
        test("localHostOrDomainIs", true, "www", "www.netscape.com");
        test("localHostOrDomainIs", false, "www.mcom.com", "www.netscape.com");
        test("localHostOrDomainIs", false, "home.netscape.com", "www.netscape.com");
    
        test("isResolvable", true, "www.netscape.com");
        test("isResolvable", false, "bogus.domain.foobar");
    
        test("isInNet", true, "198.95.249.79", "198.95.249.79", "255.255.255.255");
        test("isInNet", false, "198.95.249.78", "198.95.249.79", "255.255.255.255");
        test("isInNet", true, "198.95.249.78", "198.95.0.0", "255.255.0.0");
        test("isInNet", false, "198.96.249.78", "198.95.0.0", "255.255.0.0");
    
        console.log("Resolved " + host + ": " + dnsResolve(host));
        console.log("My IP: " + myIpAddress());
    
        test("dnsDomainLevels", 0, "www");
        test("dnsDomainLevels", 2, "www.netscape.com");
    
        test("shExpMatch", true, "http://home.netscape.com/people/ari/index.html", "*/ari/*");
        test("shExpMatch", false, "http://home.netscape.com/people/montulli/index.html", "*/ari/*");
    
        //test("weekdayRange", true, "WED");
        test("dateRange", true, "AUG", "AUG", "GMT");
        //test("timeRange", true, 16);
        //test("timeRange", true, 13, "GMT");
    
        test("proxyBindings", "{}");
    
        return "DIRECT; PROXY 127.0.0.1:8080; SOCKS 127.0.0.1:4444";
      }
    '''
    
    test = PACResolver(TEST_PAC)
    print(list(test.resolve("https://example.com/test")))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
