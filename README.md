# ocamlwarc
[WARC](https://en.wikipedia.org/wiki/Web_ARChive) parser for ocaml


See warc.mli for interface

Example usage:
```ocaml

open Cohttp

let inf = Unix.open_process_in "gunzip -c test.warc.gz" in 
Warc.iter_pages inf (fun page ->
  let rsp = Warc.get_rsp page in
  let header, http_data = rsp in 
  let rsp_head, rsp_body = Warc.parse_response_body in
  let response_status = Code.code_of_status (Response.status rsp_head) in
  if response_status == 200 then
    print_endline (Warc.get_url header)
)
```
