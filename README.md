
# msa-nginx-dashboard

Simple dashboard to display stats about the Nginx HTTP server.

![Alt text](/img/screenshot.png?raw=true "Screenshot")

The dashboard fetches stats from the [nginx-module-vts](https://github.com/vozlt/nginx-module-vts) API every second, and display them.

The javascript code to parse the JSON data is based on the original status page from nginx-module-vts.

## Installation & configuration

To add the nginx-module-vts to nginx you must compile nginx from source, and add the following arguent, pointing to the nginx-module-vts folder : **--add-module=/path/to/nginx-module-vts**.

Once Nginx is compiled, you must add the module directive to the active configuration, like this :

```nginx

  http {

      # Compute stats for all requests handled in this block
      vhost_traffic_status_zone;

      server {

          listen       80;
          server_name  localhost;

          # Serve the nginx stats from the vts module as a JSON file
          location = /nginx/stats.json {
            vhost_traffic_status_display;
            vhost_traffic_status_display_format json;
          }

          # The rest of the configuration ...
      }
  }

```

Once the stats are accessible via the **/nginx/stats.json url**, you can serve the msa-nginx-dashboard folder as a static directory, open dashboard.html in your browser,  and you should get a page similar to the screenshot above.


## TODO

- Potentially add a graph to show the evolution of the requests over time, something like : https://square.github.io/cubism/


## About

A project by the [Microservices Agency](http://microservices.agency).
