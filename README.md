# docker-lookup-service

Lookupservice accepts a list with location names and returns a list with geometries.


Example usage:

Run the docker: $ docker --name lookupservice -p 9999:8080 bde2020/lookupservice:1.0.0

Trigger it through command line: $ curl -X POST -d @post_names.json  http://localhost:9999/lookupservice/geocode -H "Content-Type:application/json" -H "Accept: application/json"

The testing file post_names.json in directory testing-files of this repo.
