golang-mux-benchmark
====================

A collection of benchmarks for popular Go web frameworks.

# Frameworks

*  [gocraft/web](https://github.com/gocraft/web)
*  [gorilla/mux](https://github.com/gorilla/mux)
*  [Martini](https://github.com/go-martini/martini)
*  [Tiger Tonic](https://github.com/rcrowley/go-tigertonic)
*  [Traffic](https://github.com/pilu/traffic)
*  [go-json-rest](https://github.com/ant0ine/go-json-rest)
*  [Goji](https://github.com/zenazn/goji/)

# Benchmarks

*  **Simple** - A single route, GET /action. Renders 'hello'.
*  **RouteN** - Where N is the total number of routes that roughly approximate a REST API. The routes are as follows:
   *  Three namespaces: /admin, /api, /site
   *  Within each namespace, N/15 resources. Each resource is a random string. Each resource specifies 5 routes:
      *  GET /resources
      *  GET /resources/:id
      *  POST /resources
      *  PUT /resources/:id
      *  DELETE /resources/:id
*  **Middleware** - Run 6 middleware functions before invoking a hello handler.
*  **Composite**
   *  6 Middleware functions
   *  150 Routes
   *  The first middleware function sets a value that the handler must read and render.

# Output

`go test -bench=. 2>/dev/null` in @cypriss's 1.8 GHz i7 Macbook Air:

```
BenchmarkGocraftWebSimple	 1000000	      2612 ns/op
BenchmarkGocraftWebRoute15	  500000	      3991 ns/op
BenchmarkGocraftWebRoute75	  500000	      4048 ns/op
BenchmarkGocraftWebRoute150	  500000	      4042 ns/op
BenchmarkGocraftWebRoute300	  500000	      4090 ns/op
BenchmarkGocraftWebRoute3000	  500000	      4597 ns/op
BenchmarkGocraftWebMiddleware	  200000	      9525 ns/op
BenchmarkGocraftWebComposite	  200000	     10165 ns/op

BenchmarkGorillaMuxSimple	  500000	      3571 ns/op
BenchmarkGorillaMuxRoute15	  100000	     18029 ns/op
BenchmarkGorillaMuxRoute75	  100000	     28711 ns/op
BenchmarkGorillaMuxRoute150	   50000	     45426 ns/op
BenchmarkGorillaMuxRoute300	   50000	     70562 ns/op
BenchmarkGorillaMuxRoute3000	    5000	    654030 ns/op

BenchmarkCodegangstaMartiniSimple	  200000	      8290 ns/op
BenchmarkCodegangstaMartiniRoute15	  100000	     15445 ns/op
BenchmarkCodegangstaMartiniRoute75	  100000	     19526 ns/op
BenchmarkCodegangstaMartiniRoute150	  100000	     23655 ns/op
BenchmarkCodegangstaMartiniRoute300	   50000	     33418 ns/op
BenchmarkCodegangstaMartiniRoute3000	   10000	    206212 ns/op
BenchmarkCodegangstaMartiniMiddleware	  100000	     18662 ns/op
BenchmarkCodegangstaMartiniComposite	   50000	     37604 ns/op

BenchmarkRcrowleyTigerTonicSimple	 5000000	       378 ns/op
BenchmarkRcrowleyTigerTonicRoute15	  200000	     26696 ns/op
BenchmarkRcrowleyTigerTonicRoute75	  500000	     14189 ns/op
BenchmarkRcrowleyTigerTonicRoute150	  500000	      9485 ns/op
BenchmarkRcrowleyTigerTonicRoute300	  500000	      7124 ns/op
BenchmarkRcrowleyTigerTonicRoute3000	  500000	      4464 ns/op

BenchmarkPiluTrafficSimple	  500000	      3624 ns/op
BenchmarkPiluTrafficRoute15	  200000	     10896 ns/op
BenchmarkPiluTrafficRoute75	  100000	     20687 ns/op
BenchmarkPiluTrafficRoute150	   50000	     33320 ns/op
BenchmarkPiluTrafficRoute300	   50000	     57293 ns/op
BenchmarkPiluTrafficRoute3000	   10000	    670427 ns/op
BenchmarkPiluTrafficMiddleware	  500000	      4102 ns/op
BenchmarkPiluTrafficComposite	   50000	     34593 ns/op
```

`go test -bench=. 2>/dev/null` in @agrison's 2.4 GHz i5 Macbook Pro (Late '13):

```
BenchmarkGocraftWeb_Simple              1000000       1022 ns/op
BenchmarkGocraftWeb_Route15             1000000       2198 ns/op
BenchmarkGocraftWeb_Route75             1000000       2233 ns/op
BenchmarkGocraftWeb_Route150            1000000       2275 ns/op
BenchmarkGocraftWeb_Route300            1000000       2349 ns/op
BenchmarkGocraftWeb_Route3000           1000000       2624 ns/op
BenchmarkGocraftWeb_Middleware          1000000       1691 ns/op
BenchmarkGocraftWeb_Composite            500000       3708 ns/op

BenchmarkGorillaMux_Simple               500000       3224 ns/op
BenchmarkGorillaMux_Route15              200000      14812 ns/op
BenchmarkGorillaMux_Route75              100000      22686 ns/op
BenchmarkGorillaMux_Route150              50000      33283 ns/op
BenchmarkGorillaMux_Route300              50000      56225 ns/op
BenchmarkGorillaMux_Route3000              5000     552553 ns/op

BenchmarkMartini_Simple                  500000       4753 ns/op
BenchmarkMartini_Route15                 200000      10414 ns/op
BenchmarkMartini_Route75                 200000      14623 ns/op
BenchmarkMartini_Route150                100000      17879 ns/op
BenchmarkMartini_Route300                100000      26418 ns/op
BenchmarkMartini_Route3000                10000     204888 ns/op
BenchmarkMartini_Middleware              100000      13971 ns/op
BenchmarkMartini_Composite                50000      30892 ns/op

BenchmarkRcrowleyTigerTonic_Simple      5000000        346 ns/op
BenchmarkRcrowleyTigerTonic_Route15      200000      23724 ns/op
BenchmarkRcrowleyTigerTonic_Route75      500000      11849 ns/op
BenchmarkRcrowleyTigerTonic_Route150     500000       8152 ns/op
BenchmarkRcrowleyTigerTonic_Route300     500000       6463 ns/op
BenchmarkRcrowleyTigerTonic_Route3000    500000       3522 ns/op

BenchmarkPiluTraffic_Simple              500000       2987 ns/op
BenchmarkPiluTraffic_Route15             200000       8683 ns/op
BenchmarkPiluTraffic_Route75             100000      16475 ns/op
BenchmarkPiluTraffic_Route150            100000      26576 ns/op
BenchmarkPiluTraffic_Route300             50000      48519 ns/op
BenchmarkPiluTraffic_Route3000            10000     556838 ns/op
BenchmarkPiluTraffic_Middleware          500000       2995 ns/op
BenchmarkPiluTraffic_Composite           100000      24672 ns/op

BenchmarkGoJsonRest_Simple               200000       5649 ns/op
BenchmarkGoJsonRest_Route15              200000       6938 ns/op
BenchmarkGoJsonRest_Route75              200000       7237 ns/op
BenchmarkGoJsonRest_Route150             200000       7357 ns/op
BenchmarkGoJsonRest_Route300             200000       8477 ns/op
BenchmarkGoJsonRest_Route3000            200000       8518 ns/op
BenchmarkGoJsonRest_Middleware           500000       5785 ns/op
BenchmarkGoJsonRest_Composite            200000       7588 ns/op

BenchmarkGoji_Simple                    5000000        579 ns/op
BenchmarkGoji_Route15                   1000000       1440 ns/op
BenchmarkGoji_Route75                   1000000       2240 ns/op
BenchmarkGoji_Route150                   500000       3237 ns/op
BenchmarkGoji_Route300                   500000       5354 ns/op
BenchmarkGoji_Route3000                   50000      40676 ns/op
BenchmarkGoji_Middleware                5000000        694 ns/op
BenchmarkGoji_Composite                  500000       3999 ns/op
```

