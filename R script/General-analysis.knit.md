
<!-- rnb-text-begin -->

---
title: "R Notebook"
output: html_notebook
---

Libraries

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHViR2xpY21GeWVTaHlaV0ZrZUd3cFhHNXNhV0p5WVhKNUtISmxZV1J5S1Z4dWJHbGljbUZ5ZVNoTllYUmphRWwwS1Z4dWJHbGljbUZ5ZVNoa2NHeDVjaWxjYm14cFluSmhjbmtvWW5KdmIyMHBYRzVzYVdKeVlYSjVLR05oY2lsY2JteHBZbkpoY25rb2NGSlBReWxjYm14cFluSmhjbmtvVW1WemIzVnlZMlZUWld4bFkzUnBiMjRwWEc1c2FXSnlZWEo1S0dadmNtVnBaMjRwWEc1Z1lHQWlmUT09IC0tPlxuXG5gYGByXG5saWJyYXJ5KHJlYWR4bClcbmxpYnJhcnkocmVhZHIpXG5saWJyYXJ5KE1hdGNoSXQpXG5saWJyYXJ5KGRwbHlyKVxubGlicmFyeShicm9vbSlcbmxpYnJhcnkoY2FyKVxubGlicmFyeShwUk9DKVxubGlicmFyeShSZXNvdXJjZVNlbGVjdGlvbilcbmxpYnJhcnkoZm9yZWlnbilcbmBgYFxuXG48IS0tIHJuYi1zb3VyY2UtZW5kIC0tPlxuIn0= -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShyZWFkeGwpXG5saWJyYXJ5KHJlYWRyKVxubGlicmFyeShNYXRjaEl0KVxubGlicmFyeShkcGx5cilcbmxpYnJhcnkoYnJvb20pXG5saWJyYXJ5KGNhcilcbmxpYnJhcnkocFJPQylcbmxpYnJhcnkoUmVzb3VyY2VTZWxlY3Rpb24pXG5saWJyYXJ5KGZvcmVpZ24pXG5gYGAifQ== -->

```r
library(readxl)
library(readr)
library(MatchIt)
library(dplyr)
library(broom)
library(car)
library(pROC)
library(ResourceSelection)
library(foreign)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Import data

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVVR0Z5ZEdsamFYQmhiblJmZEdGaWJHVmZkMmwwYUY5eVpXeGhkR1ZrWDJScGMyOXlaR1Z5Y3lBOExTQnlaV0ZrWDJWNFkyVnNLRndpTGk0dkxpNHZSR0YwWVM5UVlYSjBhV05wY0dGdWRGOTBZV0pzWlNCM2FYUm9JSEpsYkdGMFpXUWdaR2x6YjNKa1pYSnpMbmhzYzNoY0lpbGNibEJUVUY5M1gyVjRjRzl6ZFhKbGN5QThMU0J5WldGa1gyTnpkaWhjSWk0dUx5NHVMMFJoZEdFdlVGTlFYM2RmWlhod2IzTjFjbVZ6TG1OemRsd2lLVnh1VUZOUVgyRnpjMlZ6YzIxbGJuUmZZMlZ1ZEhKbElEd3RJSEpsWVdSZlkzTjJLRndpTGk0dkxpNHZSR0YwWVM5UVUxQmZZWE56WlhOemJXVnVkRjlqWlc1MGNtVXVZM04yWENJcFhHNURiMjUwY205c1gzZGZaWGh3YjNOMWNtVnpJRHd0SUhKbFlXUmZZM04yS0Z3aUxpNHZMaTR2UkdGMFlTOURiMjUwY205c1gzZGZaWGh3YjNOMWNtVnpMbU56ZGx3aUtWeHVRMjl1ZEhKdmJITmZZV2RsWDJGdVpGOXpaWGdnUEMwZ2NtVmhaRjlqYzNZb1hDSXVMaTh1TGk5RVlYUmhMME52Ym5SeWIyeHpYMkZuWlY5aGJtUmZjMlY0TG1OemRsd2lLVnh1VUUxSVgyRnVaRjl0WldSeklEd3RJSEpsWVdSZlkzTjJLRndpTGk0dkxpNHZSR0YwWVM5TlpXUWdhR2x6ZEc5eWVTQmhibVFnYldWa2N5QnpaV3htSUhKbGNHOXlkR1ZrTG1OemRsd2lLVnh1WUdCZ0luMD0gLS0+XG5cbmBgYHJcblBhcnRpY2lwYW50X3RhYmxlX3dpdGhfcmVsYXRlZF9kaXNvcmRlcnMgPC0gcmVhZF9leGNlbChcIi4uLy4uL0RhdGEvUGFydGljaXBhbnRfdGFibGUgd2l0aCByZWxhdGVkIGRpc29yZGVycy54bHN4XCIpXG5QU1Bfd19leHBvc3VyZXMgPC0gcmVhZF9jc3YoXCIuLi8uLi9EYXRhL1BTUF93X2V4cG9zdXJlcy5jc3ZcIilcblBTUF9hc3Nlc3NtZW50X2NlbnRyZSA8LSByZWFkX2NzdihcIi4uLy4uL0RhdGEvUFNQX2Fzc2Vzc21lbnRfY2VudHJlLmNzdlwiKVxuQ29udHJvbF93X2V4cG9zdXJlcyA8LSByZWFkX2NzdihcIi4uLy4uL0RhdGEvQ29udHJvbF93X2V4cG9zdXJlcy5jc3ZcIilcbkNvbnRyb2xzX2FnZV9hbmRfc2V4IDwtIHJlYWRfY3N2KFwiLi4vLi4vRGF0YS9Db250cm9sc19hZ2VfYW5kX3NleC5jc3ZcIilcblBNSF9hbmRfbWVkcyA8LSByZWFkX2NzdihcIi4uLy4uL0RhdGEvTWVkIGhpc3RvcnkgYW5kIG1lZHMgc2VsZiByZXBvcnRlZC5jc3ZcIilcbmBgYFxuXG48IS0tIHJuYi1zb3VyY2UtZW5kIC0tPlxuIn0= -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuUGFydGljaXBhbnRfdGFibGVfd2l0aF9yZWxhdGVkX2Rpc29yZGVycyA8LSByZWFkX2V4Y2VsKFwiLi4vLi4vRGF0YS9QYXJ0aWNpcGFudF90YWJsZSB3aXRoIHJlbGF0ZWQgZGlzb3JkZXJzLnhsc3hcIilcblBTUF93X2V4cG9zdXJlcyA8LSByZWFkX2NzdihcIi4uLy4uL0RhdGEvUFNQX3dfZXhwb3N1cmVzLmNzdlwiKVxuUFNQX2Fzc2Vzc21lbnRfY2VudHJlIDwtIHJlYWRfY3N2KFwiLi4vLi4vRGF0YS9QU1BfYXNzZXNzbWVudF9jZW50cmUuY3N2XCIpXG5Db250cm9sX3dfZXhwb3N1cmVzIDwtIHJlYWRfY3N2KFwiLi4vLi4vRGF0YS9Db250cm9sX3dfZXhwb3N1cmVzLmNzdlwiKVxuQ29udHJvbHNfYWdlX2FuZF9zZXggPC0gcmVhZF9jc3YoXCIuLi8uLi9EYXRhL0NvbnRyb2xzX2FnZV9hbmRfc2V4LmNzdlwiKVxuUE1IX2FuZF9tZWRzIDwtIHJlYWRfY3N2KFwiLi4vLi4vRGF0YS9NZWQgaGlzdG9yeSBhbmQgbWVkcyBzZWxmIHJlcG9ydGVkLmNzdlwiKVxuYGBgIn0= -->

```r
Participant_table_with_related_disorders <- read_excel("../../Data/Participant_table with related disorders.xlsx")
PSP_w_exposures <- read_csv("../../Data/PSP_w_exposures.csv")
PSP_assessment_centre <- read_csv("../../Data/PSP_assessment_centre.csv")
Control_w_exposures <- read_csv("../../Data/Control_w_exposures.csv")
Controls_age_and_sex <- read_csv("../../Data/Controls_age_and_sex.csv")
PMH_and_meds <- read_csv("../../Data/Med history and meds self reported.csv")
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Combine groups into PSP and healthy cohorts, then combine into single dataframe


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVRMjl1ZEhKdmJITmZZV3hzSUR3dElHMWxjbWRsS0VOdmJuUnliMnhmZDE5bGVIQnZjM1Z5WlhNc1hHNGdJQ0FnSUNBZ0lDQWdJQ0FnSUNBZ0lDQWdJQ0FnUTI5dWRISnZiSE5mWVdkbFgyRnVaRjl6Wlhnc1hHNGdJQ0FnSUNBZ0lDQWdJQ0FnSUNBZ0lDQWdJQ0FnWW5rZ1BTQmNJbEJoY25ScFkybHdZVzUwSUVsRVhDSXBYRzVEYjI1MGNtOXNjMTloYkd3Z1BDMGdiV1Z5WjJVb1EyOXVkSEp2YkhOZllXeHNMRnh1SUNBZ0lDQWdJQ0FnSUNBZ0lDQWdJQ0FnSUNBZ0lGQk5TRjloYm1SZmJXVmtjeXhjYmlBZ0lDQWdJQ0FnSUNBZ0lDQWdJQ0FnSUNBZ0lDQmllU0E5SUZ3aVVHRnlkR2xqYVhCaGJuUWdTVVJjSWlsY2JsQlRVRjloYkd3Z1BDMGdiV1Z5WjJVb1VGTlFYM2RmWlhod2IzTjFjbVZ6TEZ4dUlDQWdJQ0FnSUNBZ0lDQWdJQ0FnSUNCUVlYSjBhV05wY0dGdWRGOTBZV0pzWlY5M2FYUm9YM0psYkdGMFpXUmZaR2x6YjNKa1pYSnpMRnh1SUNBZ0lDQWdJQ0FnSUNBZ0lDQWdJQ0JpZVNBOUlGd2lVR0Z5ZEdsamFYQmhiblFnU1VSY0lpbGNibEJUVUY5aGJHd2dQQzBnYldWeVoyVW9VRk5RWDJGc2JDeGNiaUFnSUNBZ0lDQWdJQ0FnSUNBZ0lDQWdVRk5RWDJGemMyVnpjMjFsYm5SZlkyVnVkSEpsTEZ4dUlDQWdJQ0FnSUNBZ0lDQWdJQ0FnSUNCaWVTQTlJRndpVUdGeWRHbGphWEJoYm5RZ1NVUmNJaWxjYmxCVFVGOWhiR3hmZDE5d2JXZ2dQQzBnYldWeVoyVW9VRk5RWDJGc2JDeGNiaUFnSUNBZ0lDQWdJQ0FnSUNBZ0lDQWdVRTFJWDJGdVpGOXRaV1J6TEZ4dUlDQWdJQ0FnSUNBZ0lDQWdJQ0FnSUNCaWVTQTlJRndpVUdGeWRHbGphWEJoYm5RZ1NVUmNJaWxjYm1sbUlDaGNJbFZMSUVKcGIySmhibXNnWVhOelpYTnpiV1Z1ZENCalpXNTBjbVVnZkNCSmJuTjBZVzVqWlNBd0xubGNJaUFsYVc0bElHNWhiV1Z6S0ZCVFVGOWhiR3dwS1NCN0lDTkdhWGdnYm1GdFpTQmthWE5qY21Wd1lXNWplVnh1SUNCUVUxQmZZV3hzSUR3dElGQlRVRjloYkd4ZmQxOXdiV2dnSlQ0bFhHNGdJQ0FnY21WdVlXMWxLR0JWU3lCQ2FXOWlZVzVySUdGemMyVnpjMjFsYm5RZ1kyVnVkSEpsSUh3Z1NXNXpkR0Z1WTJVZ01HQWdQVnh1SUNBZ0lDQWdJQ0FnSUNBZ0lHQlZTeUJDYVc5aVlXNXJJR0Z6YzJWemMyMWxiblFnWTJWdWRISmxJSHdnU1c1emRHRnVZMlVnTUM1NVlDbGNibjFjYm1CZ1lDSjkgLS0+XG5cbmBgYHJcbkNvbnRyb2xzX2FsbCA8LSBtZXJnZShDb250cm9sX3dfZXhwb3N1cmVzLFxuICAgICAgICAgICAgICAgICAgICAgIENvbnRyb2xzX2FnZV9hbmRfc2V4LFxuICAgICAgICAgICAgICAgICAgICAgIGJ5ID0gXCJQYXJ0aWNpcGFudCBJRFwiKVxuQ29udHJvbHNfYWxsIDwtIG1lcmdlKENvbnRyb2xzX2FsbCxcbiAgICAgICAgICAgICAgICAgICAgICBQTUhfYW5kX21lZHMsXG4gICAgICAgICAgICAgICAgICAgICAgYnkgPSBcIlBhcnRpY2lwYW50IElEXCIpXG5QU1BfYWxsIDwtIG1lcmdlKFBTUF93X2V4cG9zdXJlcyxcbiAgICAgICAgICAgICAgICAgUGFydGljaXBhbnRfdGFibGVfd2l0aF9yZWxhdGVkX2Rpc29yZGVycyxcbiAgICAgICAgICAgICAgICAgYnkgPSBcIlBhcnRpY2lwYW50IElEXCIpXG5QU1BfYWxsIDwtIG1lcmdlKFBTUF9hbGwsXG4gICAgICAgICAgICAgICAgIFBTUF9hc3Nlc3NtZW50X2NlbnRyZSxcbiAgICAgICAgICAgICAgICAgYnkgPSBcIlBhcnRpY2lwYW50IElEXCIpXG5QU1BfYWxsX3dfcG1oIDwtIG1lcmdlKFBTUF9hbGwsXG4gICAgICAgICAgICAgICAgIFBNSF9hbmRfbWVkcyxcbiAgICAgICAgICAgICAgICAgYnkgPSBcIlBhcnRpY2lwYW50IElEXCIpXG5pZiAoXCJVSyBCaW9iYW5rIGFzc2Vzc21lbnQgY2VudHJlIHwgSW5zdGFuY2UgMC55XCIgJWluJSBuYW1lcyhQU1BfYWxsKSkgeyAjRml4IG5hbWUgZGlzY3JlcGFuY3lcbiAgUFNQX2FsbCA8LSBQU1BfYWxsX3dfcG1oICU+JVxuICAgIHJlbmFtZShgVUsgQmlvYmFuayBhc3Nlc3NtZW50IGNlbnRyZSB8IEluc3RhbmNlIDBgID1cbiAgICAgICAgICAgICBgVUsgQmlvYmFuayBhc3Nlc3NtZW50IGNlbnRyZSB8IEluc3RhbmNlIDAueWApXG59XG5gYGBcblxuPCEtLSBybmItc291cmNlLWVuZCAtLT5cbiJ9 -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuQ29udHJvbHNfYWxsIDwtIG1lcmdlKENvbnRyb2xfd19leHBvc3VyZXMsXG4gICAgICAgICAgICAgICAgICAgICAgQ29udHJvbHNfYWdlX2FuZF9zZXgsXG4gICAgICAgICAgICAgICAgICAgICAgYnkgPSBcIlBhcnRpY2lwYW50IElEXCIpXG5Db250cm9sc19hbGwgPC0gbWVyZ2UoQ29udHJvbHNfYWxsLFxuICAgICAgICAgICAgICAgICAgICAgIFBNSF9hbmRfbWVkcyxcbiAgICAgICAgICAgICAgICAgICAgICBieSA9IFwiUGFydGljaXBhbnQgSURcIilcblBTUF9hbGwgPC0gbWVyZ2UoUFNQX3dfZXhwb3N1cmVzLFxuICAgICAgICAgICAgICAgICBQYXJ0aWNpcGFudF90YWJsZV93aXRoX3JlbGF0ZWRfZGlzb3JkZXJzLFxuICAgICAgICAgICAgICAgICBieSA9IFwiUGFydGljaXBhbnQgSURcIilcblBTUF9hbGwgPC0gbWVyZ2UoUFNQX2FsbCxcbiAgICAgICAgICAgICAgICAgUFNQX2Fzc2Vzc21lbnRfY2VudHJlLFxuICAgICAgICAgICAgICAgICBieSA9IFwiUGFydGljaXBhbnQgSURcIilcblBTUF9hbGxfd19wbWggPC0gbWVyZ2UoUFNQX2FsbCxcbiAgICAgICAgICAgICAgICAgUE1IX2FuZF9tZWRzLFxuICAgICAgICAgICAgICAgICBieSA9IFwiUGFydGljaXBhbnQgSURcIilcbmlmIChcIlVLIEJpb2JhbmsgYXNzZXNzbWVudCBjZW50cmUgfCBJbnN0YW5jZSAwLnlcIiAlaW4lIG5hbWVzKFBTUF9hbGwpKSB7ICNGaXggbmFtZSBkaXNjcmVwYW5jeVxuICBQU1BfYWxsIDwtIFBTUF9hbGxfd19wbWggJT4lXG4gICAgcmVuYW1lKGBVSyBCaW9iYW5rIGFzc2Vzc21lbnQgY2VudHJlIHwgSW5zdGFuY2UgMGAgPVxuICAgICAgICAgICAgIGBVSyBCaW9iYW5rIGFzc2Vzc21lbnQgY2VudHJlIHwgSW5zdGFuY2UgMC55YClcbn1cbmBgYCJ9 -->

```r
Controls_all <- merge(Control_w_exposures,
                      Controls_age_and_sex,
                      by = "Participant ID")
Controls_all <- merge(Controls_all,
                      PMH_and_meds,
                      by = "Participant ID")
PSP_all <- merge(PSP_w_exposures,
                 Participant_table_with_related_disorders,
                 by = "Participant ID")
PSP_all <- merge(PSP_all,
                 PSP_assessment_centre,
                 by = "Participant ID")
PSP_all_w_pmh <- merge(PSP_all,
                 PMH_and_meds,
                 by = "Participant ID")
if ("UK Biobank assessment centre | Instance 0.y" %in% names(PSP_all)) { #Fix name discrepancy
  PSP_all <- PSP_all_w_pmh %>%
    rename(`UK Biobank assessment centre | Instance 0` =
             `UK Biobank assessment centre | Instance 0.y`)
}
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Combine into one dataframe

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVjSE53SUNBOExTQlFVMUJmWVd4c0lDVStKU0J0ZFhSaGRHVW9ZMkZ6WlNBOUlERk1LVnh1WTNSeWJDQThMU0JEYjI1MGNtOXNjMTloYkd3Z0pUNGxJRzExZEdGMFpTaGpZWE5sSUQwZ01Fd3BYRzVrWmlBOExTQmlhVzVrWDNKdmQzTW9jSE53TEdOMGNtd3BYRzVnWUdBaWZRPT0gLS0+XG5cbmBgYHJcbnBzcCAgPC0gUFNQX2FsbCAlPiUgbXV0YXRlKGNhc2UgPSAxTClcbmN0cmwgPC0gQ29udHJvbHNfYWxsICU+JSBtdXRhdGUoY2FzZSA9IDBMKVxuZGYgPC0gYmluZF9yb3dzKHBzcCxjdHJsKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucHNwICA8LSBQU1BfYWxsICU+JSBtdXRhdGUoY2FzZSA9IDFMKVxuY3RybCA8LSBDb250cm9sc19hbGwgJT4lIG11dGF0ZShjYXNlID0gMEwpXG5kZiA8LSBiaW5kX3Jvd3MocHNwLGN0cmwpXG5gYGAifQ== -->

```r
psp  <- PSP_all %>% mutate(case = 1L)
ctrl <- Controls_all %>% mutate(case = 0L)
df <- bind_rows(psp,ctrl)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Make matched control group, matched on age, sex, and assessment center, at 10:1 ratio

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHViU0E4TFNCdFlYUmphR2wwS0Z4dUlDQmpZWE5sSUg0Z1lGTmxlR0FnS3lCZ1FXZGxJR0YwSUhKbFkzSjFhWFJ0Wlc1MFlDQXJJR0JWU3lCQ2FXOWlZVzVySUdGemMyVnpjMjFsYm5RZ1kyVnVkSEpsSUh3Z1NXNXpkR0Z1WTJVZ01HQXNYRzRnSUdSaGRHRWdQU0JrWml4Y2JpQWdiV1YwYUc5a0lEMGdYQ0p1WldGeVpYTjBYQ0lzWEc0Z0lHUnBjM1JoYm1ObElEMGdYQ0puYkcxY0lpeGNiaUFnY21GMGFXOGdQU0F4TUZ4dUtWeHVYRzV6ZFcxdFlYSjVLRzBwWEc1Y2JtMWhkR05vWldSZllXeHNJRHd0SUcxaGRHTm9MbVJoZEdFb2JTbGNibUJnWUNKOSAtLT5cblxuYGBgclxubSA8LSBtYXRjaGl0KFxuICBjYXNlIH4gYFNleGAgKyBgQWdlIGF0IHJlY3J1aXRtZW50YCArIGBVSyBCaW9iYW5rIGFzc2Vzc21lbnQgY2VudHJlIHwgSW5zdGFuY2UgMGAsXG4gIGRhdGEgPSBkZixcbiAgbWV0aG9kID0gXCJuZWFyZXN0XCIsXG4gIGRpc3RhbmNlID0gXCJnbG1cIixcbiAgcmF0aW8gPSAxMFxuKVxuXG5zdW1tYXJ5KG0pXG5cbm1hdGNoZWRfYWxsIDwtIG1hdGNoLmRhdGEobSlcbmBgYFxuXG48IS0tIHJuYi1zb3VyY2UtZW5kIC0tPlxuIn0= -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubSA8LSBtYXRjaGl0KFxuICBjYXNlIH4gYFNleGAgKyBgQWdlIGF0IHJlY3J1aXRtZW50YCArIGBVSyBCaW9iYW5rIGFzc2Vzc21lbnQgY2VudHJlIHwgSW5zdGFuY2UgMGAsXG4gIGRhdGEgPSBkZixcbiAgbWV0aG9kID0gXCJuZWFyZXN0XCIsXG4gIGRpc3RhbmNlID0gXCJnbG1cIixcbiAgcmF0aW8gPSAxMFxuKVxuXG5zdW1tYXJ5KG0pXG5cbm1hdGNoZWRfYWxsIDwtIG1hdGNoLmRhdGEobSlcbmBgYCJ9 -->

```r
m <- matchit(
  case ~ `Sex` + `Age at recruitment` + `UK Biobank assessment centre | Instance 0`,
  data = df,
  method = "nearest",
  distance = "glm",
  ratio = 10
)

summary(m)

matched_all <- match.data(m)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



Analysis - see if CVD is more common in PSP than controls (by self report)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVZM1prWDNSaFlteGxJRHd0SUcxaGRHTm9aV1JmWVd4c0lDVStKVnh1SUNCelpXeGxZM1FvWUZCaGNuUnBZMmx3WVc1MElFbEVZQ3dnWEc0Z0lDQWdJQ0FnSUNCZ1kyRnpaV0FzWEc0Z0lDQWdJQ0FnSUNCamRtUmZkbUZ5SUQwZ1lGWmhjMk4xYkdGeUwyaGxZWEowSUhCeWIySnNaVzF6SUdScFlXZHViM05sWkNCaWVTQmtiMk4wYjNJZ2ZDQkpibk4wWVc1alpTQXdZQ2tnSlQ0bFhHNGdJR1pwYkhSbGNpaGpkbVJmZG1GeUlDRTlJRndpVUhKbFptVnlJRzV2ZENCMGJ5Qmhibk4zWlhKY0lpa2dKVDRsWEc0Z0lHMTFkR0YwWlNob1lYTmZZM1prSUQwZ2FXWmZaV3h6WlNoamRtUmZkbUZ5SUQwOUlGd2lUbTl1WlNCdlppQjBhR1VnWVdKdmRtVmNJaXdnTUV3c0lERk1LU2xjYmx4dVkzWmtYM04xYlcxaGNua2dQQzBnWTNaa1gzUmhZbXhsSUNVK0pWeHVJQ0JuY205MWNGOWllU2hqWVhObEtTQWxQaVZjYmlBZ2MzVnRiV0Z5YVhObEtGeHVJQ0FnSUc0Z1BTQnVLQ2tzWEc0Z0lDQWdibDkzYVhSb1gyTjJaQ0E5SUhOMWJTaG9ZWE5mWTNaa0tTeGNiaUFnSUNCd1pYSmpaVzUwWDNkcGRHaGZZM1prSUQwZ01UQXdJQ29nYldWaGJpaG9ZWE5mWTNaa0tTeGNiaUFnSUNBdVozSnZkWEJ6SUQwZ1hDSmtjbTl3WENKY2JpQWdLVnh1WEc1amRtUmZkR0ZpSUR3dElIUmhZbXhsS0dOMlpGOTBZV0pzWlNSallYTmxMQ0JqZG1SZmRHRmliR1VrYUdGelgyTjJaQ2xjYm1Ob2FYTnhMblJsYzNRb1kzWmtYM1JoWWlsY2JtQmdZQ0o5IC0tPlxuXG5gYGByXG5jdmRfdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgIGN2ZF92YXIgPSBgVmFzY3VsYXIvaGVhcnQgcHJvYmxlbXMgZGlhZ25vc2VkIGJ5IGRvY3RvciB8IEluc3RhbmNlIDBgKSAlPiVcbiAgZmlsdGVyKGN2ZF92YXIgIT0gXCJQcmVmZXIgbm90IHRvIGFuc3dlclwiKSAlPiVcbiAgbXV0YXRlKGhhc19jdmQgPSBpZl9lbHNlKGN2ZF92YXIgPT0gXCJOb25lIG9mIHRoZSBhYm92ZVwiLCAwTCwgMUwpKVxuXG5jdmRfc3VtbWFyeSA8LSBjdmRfdGFibGUgJT4lXG4gIGdyb3VwX2J5KGNhc2UpICU+JVxuICBzdW1tYXJpc2UoXG4gICAgbiA9IG4oKSxcbiAgICBuX3dpdGhfY3ZkID0gc3VtKGhhc19jdmQpLFxuICAgIHBlcmNlbnRfd2l0aF9jdmQgPSAxMDAgKiBtZWFuKGhhc19jdmQpLFxuICAgIC5ncm91cHMgPSBcImRyb3BcIlxuICApXG5cbmN2ZF90YWIgPC0gdGFibGUoY3ZkX3RhYmxlJGNhc2UsIGN2ZF90YWJsZSRoYXNfY3ZkKVxuY2hpc3EudGVzdChjdmRfdGFiKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY3ZkX3RhYmxlIDwtIG1hdGNoZWRfYWxsICU+JVxuICBzZWxlY3QoYFBhcnRpY2lwYW50IElEYCwgXG4gICAgICAgICBgY2FzZWAsXG4gICAgICAgICBjdmRfdmFyID0gYFZhc2N1bGFyL2hlYXJ0IHByb2JsZW1zIGRpYWdub3NlZCBieSBkb2N0b3IgfCBJbnN0YW5jZSAwYCkgJT4lXG4gIGZpbHRlcihjdmRfdmFyICE9IFwiUHJlZmVyIG5vdCB0byBhbnN3ZXJcIikgJT4lXG4gIG11dGF0ZShoYXNfY3ZkID0gaWZfZWxzZShjdmRfdmFyID09IFwiTm9uZSBvZiB0aGUgYWJvdmVcIiwgMEwsIDFMKSlcblxuY3ZkX3N1bW1hcnkgPC0gY3ZkX3RhYmxlICU+JVxuICBncm91cF9ieShjYXNlKSAlPiVcbiAgc3VtbWFyaXNlKFxuICAgIG4gPSBuKCksXG4gICAgbl93aXRoX2N2ZCA9IHN1bShoYXNfY3ZkKSxcbiAgICBwZXJjZW50X3dpdGhfY3ZkID0gMTAwICogbWVhbihoYXNfY3ZkKSxcbiAgICAuZ3JvdXBzID0gXCJkcm9wXCJcbiAgKVxuXG5jdmRfdGFiIDwtIHRhYmxlKGN2ZF90YWJsZSRjYXNlLCBjdmRfdGFibGUkaGFzX2N2ZClcbmNoaXNxLnRlc3QoY3ZkX3RhYilcbmBgYCJ9 -->

```r
cvd_table <- matched_all %>%
  select(`Participant ID`, 
         `case`,
         cvd_var = `Vascular/heart problems diagnosed by doctor | Instance 0`) %>%
  filter(cvd_var != "Prefer not to answer") %>%
  mutate(has_cvd = if_else(cvd_var == "None of the above", 0L, 1L))

cvd_summary <- cvd_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    n_with_cvd = sum(has_cvd),
    percent_with_cvd = 100 * mean(has_cvd),
    .groups = "drop"
  )

cvd_tab <- table(cvd_table$case, cvd_table$has_cvd)
chisq.test(cvd_tab)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5cdFBlYXJzb24ncyBDaGktc3F1YXJlZCB0ZXN0IHdpdGggWWF0ZXMnIGNvbnRpbnVpdHkgY29ycmVjdGlvblxuXG5kYXRhOiAgY3ZkX3RhYlxuWC1zcXVhcmVkID0gMy43ODE1LCBkZiA9IDEsIHAtdmFsdWUgPSAwLjA1MTgyXG4ifQ== -->

```

	Pearson's Chi-squared test with Yates' continuity correction

data:  cvd_tab
X-squared = 3.7815, df = 1, p-value = 0.05182
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVZM1prWDNSaFlseHVZR0JnSW4wPSAtLT5cblxuYGBgclxuY3ZkX3RhYlxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY3ZkX3RhYlxuYGBgIn0= -->

```r
cvd_tab
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgXG4gICAgICAgMCAgICAxXG4gIDAgMTQ5NyAgOTcxXG4gIDEgIDEzMyAgMTEzXG4ifQ== -->

```
   
       0    1
  0 1497  971
  1  133  113
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVaR2x0Ym1GdFpYTW9ZM1prWDNSaFlpQThMU0JzYVhOMEtGeHVJQ0JEWVhObFUzUmhkSFZ6SUQwZ1l5aGNJa052Ym5SeWIyeGNJaXdnWENKRFlYTmxYQ0lwTENBZ0lDQWdJQ01nY205M0lHNWhiV1Z6WEc0Z0lGTmxiR1pTWlhCdmNuUmxaRU5XUkNBZ0lDQTlJR01vWENKT2Ixd2lMQ0JjSWxsbGMxd2lLU0FnSUNBZ0lDQWdJQ0FnSUNBaklHTnZiQ0J1WVcxbGMxeHVJQ0FwSUZ4dUtWeHVZR0JnSW4wPSAtLT5cblxuYGBgclxuZGltbmFtZXMoY3ZkX3RhYiA8LSBsaXN0KFxuICBDYXNlU3RhdHVzID0gYyhcIkNvbnRyb2xcIiwgXCJDYXNlXCIpLCAgICAgICMgcm93IG5hbWVzXG4gIFNlbGZSZXBvcnRlZENWRCAgICA9IGMoXCJOb1wiLCBcIlllc1wiKSAgICAgICAgICAgICAjIGNvbCBuYW1lc1xuICApIFxuKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGltbmFtZXMoY3ZkX3RhYiA8LSBsaXN0KFxuICBDYXNlU3RhdHVzID0gYyhcIkNvbnRyb2xcIiwgXCJDYXNlXCIpLCAgICAgICMgcm93IG5hbWVzXG4gIFNlbGZSZXBvcnRlZENWRCAgICA9IGMoXCJOb1wiLCBcIlllc1wiKSAgICAgICAgICAgICAjIGNvbCBuYW1lc1xuICApIFxuKVxuYGBgIn0= -->

```r
dimnames(cvd_tab <- list(
  CaseStatus = c("Control", "Case"),      # row names
  SelfReportedCVD    = c("No", "Yes")             # col names
  ) 
)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiTlVMTFxuIn0= -->

```
NULL
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Analysis - see if self-reported HTN is more common in PSP than controls (run the CVD one above first)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVhSFJ1WDNSaFlteGxJRHd0SUdOMlpGOTBZV0pzWlNBbFBpVmNiaUFnYlhWMFlYUmxLR2hoYzE5b2RHNGdQU0JwWmw5bGJITmxLRnh1SUNBZ0lITjBjbDlrWlhSbFkzUW9ZM1prWDNaaGNpd2djbVZuWlhnb1hDSklhV2RvSUdKc2IyOWtJSEJ5WlhOemRYSmxYQ0lzSUdsbmJtOXlaVjlqWVhObElEMGdWRkpWUlNrcExDQXhUQ3dnTUV3cEtWeHVYRzVvZEc1ZmMzVnRiV0Z5ZVNBOExTQm9kRzVmZEdGaWJHVWdKVDRsWEc0Z0lHZHliM1Z3WDJKNUtHTmhjMlVwSUNVK0pWeHVJQ0J6ZFcxdFlYSnBjMlVvWEc0Z0lDQWdiaUE5SUc0b0tTeGNiaUFnSUNCdVgzZHBkR2hmYUhSdUlEMGdjM1Z0S0doaGMxOW9kRzRwTEZ4dUlDQWdJSEJsY21ObGJuUmZkMmwwYUY5b2RHNGdQU0F4TURBZ0tpQnRaV0Z1S0doaGMxOW9kRzRwTEZ4dUlDQWdJQzVuY205MWNITWdQU0JjSW1SeWIzQmNJbHh1SUNBcFhHNWNibWgwYmw5MFlXSWdQQzBnZEdGaWJHVW9hSFJ1WDNSaFlteGxKR05oYzJVc0lHaDBibDkwWVdKc1pTUm9ZWE5mYUhSdUtWeHVhSFJ1WDNSaFlseHVZR0JnSW4wPSAtLT5cblxuYGBgclxuaHRuX3RhYmxlIDwtIGN2ZF90YWJsZSAlPiVcbiAgbXV0YXRlKGhhc19odG4gPSBpZl9lbHNlKFxuICAgIHN0cl9kZXRlY3QoY3ZkX3ZhciwgcmVnZXgoXCJIaWdoIGJsb29kIHByZXNzdXJlXCIsIGlnbm9yZV9jYXNlID0gVFJVRSkpLCAxTCwgMEwpKVxuXG5odG5fc3VtbWFyeSA8LSBodG5fdGFibGUgJT4lXG4gIGdyb3VwX2J5KGNhc2UpICU+JVxuICBzdW1tYXJpc2UoXG4gICAgbiA9IG4oKSxcbiAgICBuX3dpdGhfaHRuID0gc3VtKGhhc19odG4pLFxuICAgIHBlcmNlbnRfd2l0aF9odG4gPSAxMDAgKiBtZWFuKGhhc19odG4pLFxuICAgIC5ncm91cHMgPSBcImRyb3BcIlxuICApXG5cbmh0bl90YWIgPC0gdGFibGUoaHRuX3RhYmxlJGNhc2UsIGh0bl90YWJsZSRoYXNfaHRuKVxuaHRuX3RhYlxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuaHRuX3RhYmxlIDwtIGN2ZF90YWJsZSAlPiVcbiAgbXV0YXRlKGhhc19odG4gPSBpZl9lbHNlKFxuICAgIHN0cl9kZXRlY3QoY3ZkX3ZhciwgcmVnZXgoXCJIaWdoIGJsb29kIHByZXNzdXJlXCIsIGlnbm9yZV9jYXNlID0gVFJVRSkpLCAxTCwgMEwpKVxuXG5odG5fc3VtbWFyeSA8LSBodG5fdGFibGUgJT4lXG4gIGdyb3VwX2J5KGNhc2UpICU+JVxuICBzdW1tYXJpc2UoXG4gICAgbiA9IG4oKSxcbiAgICBuX3dpdGhfaHRuID0gc3VtKGhhc19odG4pLFxuICAgIHBlcmNlbnRfd2l0aF9odG4gPSAxMDAgKiBtZWFuKGhhc19odG4pLFxuICAgIC5ncm91cHMgPSBcImRyb3BcIlxuICApXG5cbmh0bl90YWIgPC0gdGFibGUoaHRuX3RhYmxlJGNhc2UsIGh0bl90YWJsZSRoYXNfaHRuKVxuaHRuX3RhYlxuYGBgIn0= -->

```r
htn_table <- cvd_table %>%
  mutate(has_htn = if_else(
    str_detect(cvd_var, regex("High blood pressure", ignore_case = TRUE)), 1L, 0L))

htn_summary <- htn_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    n_with_htn = sum(has_htn),
    percent_with_htn = 100 * mean(has_htn),
    .groups = "drop"
  )

htn_tab <- table(htn_table$case, htn_table$has_htn)
htn_tab
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgXG4gICAgICAgMCAgICAxXG4gIDAgMTYyMCAgODQ4XG4gIDEgIDE1MiAgIDk0XG4ifQ== -->

```
   
       0    1
  0 1620  848
  1  152   94
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVZMmhwYzNFdWRHVnpkQ2hvZEc1ZmRHRmlLVnh1WUdCZ0luMD0gLS0+XG5cbmBgYHJcbmNoaXNxLnRlc3QoaHRuX3RhYilcbmBgYFxuXG48IS0tIHJuYi1zb3VyY2UtZW5kIC0tPlxuIn0= -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY2hpc3EudGVzdChodG5fdGFiKVxuYGBgIn0= -->

```r
chisq.test(htn_tab)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5cdFBlYXJzb24ncyBDaGktc3F1YXJlZCB0ZXN0IHdpdGggWWF0ZXMnIGNvbnRpbnVpdHkgY29ycmVjdGlvblxuXG5kYXRhOiAgaHRuX3RhYlxuWC1zcXVhcmVkID0gMS4yOTkzLCBkZiA9IDEsIHAtdmFsdWUgPSAwLjI1NDNcbiJ9 -->

```

	Pearson's Chi-squared test with Yates' continuity correction

data:  htn_tab
X-squared = 1.2993, df = 1, p-value = 0.2543
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Analysis - see if self-reported diabetes is more common in PSP than controls

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVaRzFmZEdGaWJHVWdQQzBnYldGMFkyaGxaRjloYkd3Z0pUNGxYRzRnSUhObGJHVmpkQ2hnVUdGeWRHbGphWEJoYm5RZ1NVUmdMQ0JjYmlBZ0lDQWdJQ0FnSUdCallYTmxZQ3hjYmlBZ0lDQWdJQ0FnSUdSdFgzWmhjaUE5SUdCRWFXRmlaWFJsY3lCa2FXRm5ibTl6WldRZ1lua2daRzlqZEc5eUlId2dTVzV6ZEdGdVkyVWdNR0FwSUNVK0pWeHVJQ0JtYVd4MFpYSW9aRzFmZG1GeUlDRTlJRndpVUhKbFptVnlJRzV2ZENCMGJ5Qmhibk4zWlhKY0lpa2dKVDRsWEc0Z0lHWnBiSFJsY2loa2JWOTJZWElnSVQwZ1hDSkVieUJ1YjNRZ2EyNXZkMXdpS1NBbFBpVmNiaUFnYlhWMFlYUmxLR2hoYzE5a2JTQTlJR2xtWDJWc2MyVW9aRzFmZG1GeUlEMDlJRndpVG05Y0lpd2dNRXdzSURGTUtTbGNibHh1WkcxZmMzVnRiV0Z5ZVNBOExTQmtiVjkwWVdKc1pTQWxQaVZjYmlBZ1ozSnZkWEJmWW5rb1kyRnpaU2tnSlQ0bFhHNGdJSE4xYlcxaGNtbHpaU2hjYmlBZ0lDQnVJRDBnYmlncExGeHVJQ0FnSUc1ZmQybDBhRjlrYlNBOUlITjFiU2hvWVhOZlpHMHBMRnh1SUNBZ0lIQmxjbU5sYm5SZmQybDBhRjlrYlNBOUlERXdNQ0FxSUcxbFlXNG9hR0Z6WDJSdEtTeGNiaUFnSUNBdVozSnZkWEJ6SUQwZ1hDSmtjbTl3WENKY2JpQWdLVnh1WEc1a2JWOTBZV0lnUEMwZ2RHRmliR1VvWkcxZmRHRmliR1VrWTJGelpTd2daRzFmZEdGaWJHVWthR0Z6WDJSdEtWeHVaRzFmZEdGaVhHNWdZR0FpZlE9PSAtLT5cblxuYGBgclxuZG1fdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgIGRtX3ZhciA9IGBEaWFiZXRlcyBkaWFnbm9zZWQgYnkgZG9jdG9yIHwgSW5zdGFuY2UgMGApICU+JVxuICBmaWx0ZXIoZG1fdmFyICE9IFwiUHJlZmVyIG5vdCB0byBhbnN3ZXJcIikgJT4lXG4gIGZpbHRlcihkbV92YXIgIT0gXCJEbyBub3Qga25vd1wiKSAlPiVcbiAgbXV0YXRlKGhhc19kbSA9IGlmX2Vsc2UoZG1fdmFyID09IFwiTm9cIiwgMEwsIDFMKSlcblxuZG1fc3VtbWFyeSA8LSBkbV90YWJsZSAlPiVcbiAgZ3JvdXBfYnkoY2FzZSkgJT4lXG4gIHN1bW1hcmlzZShcbiAgICBuID0gbigpLFxuICAgIG5fd2l0aF9kbSA9IHN1bShoYXNfZG0pLFxuICAgIHBlcmNlbnRfd2l0aF9kbSA9IDEwMCAqIG1lYW4oaGFzX2RtKSxcbiAgICAuZ3JvdXBzID0gXCJkcm9wXCJcbiAgKVxuXG5kbV90YWIgPC0gdGFibGUoZG1fdGFibGUkY2FzZSwgZG1fdGFibGUkaGFzX2RtKVxuZG1fdGFiXG5gYGBcblxuPCEtLSBybmItc291cmNlLWVuZCAtLT5cbiJ9 -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZG1fdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgIGRtX3ZhciA9IGBEaWFiZXRlcyBkaWFnbm9zZWQgYnkgZG9jdG9yIHwgSW5zdGFuY2UgMGApICU+JVxuICBmaWx0ZXIoZG1fdmFyICE9IFwiUHJlZmVyIG5vdCB0byBhbnN3ZXJcIikgJT4lXG4gIGZpbHRlcihkbV92YXIgIT0gXCJEbyBub3Qga25vd1wiKSAlPiVcbiAgbXV0YXRlKGhhc19kbSA9IGlmX2Vsc2UoZG1fdmFyID09IFwiTm9cIiwgMEwsIDFMKSlcblxuZG1fc3VtbWFyeSA8LSBkbV90YWJsZSAlPiVcbiAgZ3JvdXBfYnkoY2FzZSkgJT4lXG4gIHN1bW1hcmlzZShcbiAgICBuID0gbigpLFxuICAgIG5fd2l0aF9kbSA9IHN1bShoYXNfZG0pLFxuICAgIHBlcmNlbnRfd2l0aF9kbSA9IDEwMCAqIG1lYW4oaGFzX2RtKSxcbiAgICAuZ3JvdXBzID0gXCJkcm9wXCJcbiAgKVxuXG5kbV90YWIgPC0gdGFibGUoZG1fdGFibGUkY2FzZSwgZG1fdGFibGUkaGFzX2RtKVxuZG1fdGFiXG5gYGAifQ== -->

```r
dm_table <- matched_all %>%
  select(`Participant ID`, 
         `case`,
         dm_var = `Diabetes diagnosed by doctor | Instance 0`) %>%
  filter(dm_var != "Prefer not to answer") %>%
  filter(dm_var != "Do not know") %>%
  mutate(has_dm = if_else(dm_var == "No", 0L, 1L))

dm_summary <- dm_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    n_with_dm = sum(has_dm),
    percent_with_dm = 100 * mean(has_dm),
    .groups = "drop"
  )

dm_tab <- table(dm_table$case, dm_table$has_dm)
dm_tab
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgXG4gICAgICAgMCAgICAxXG4gIDAgMjI4OCAgMTc5XG4gIDEgIDIyNyAgIDE4XG4ifQ== -->

```
   
       0    1
  0 2288  179
  1  227   18
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVZMmhwYzNFdWRHVnpkQ2hrYlY5MFlXSXBYRzVnWUdBaWZRPT0gLS0+XG5cbmBgYHJcbmNoaXNxLnRlc3QoZG1fdGFiKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY2hpc3EudGVzdChkbV90YWIpXG5gYGAifQ== -->

```r
chisq.test(dm_tab)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5cdFBlYXJzb24ncyBDaGktc3F1YXJlZCB0ZXN0IHdpdGggWWF0ZXMnIGNvbnRpbnVpdHkgY29ycmVjdGlvblxuXG5kYXRhOiAgZG1fdGFiXG5YLXNxdWFyZWQgPSAxLjkyNDNlLTI3LCBkZiA9IDEsIHAtdmFsdWUgPSAxXG4ifQ== -->

```

	Pearson's Chi-squared test with Yates' continuity correction

data:  dm_tab
X-squared = 1.9243e-27, df = 1, p-value = 1
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

Analysis - number of diagnoses and meds

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHViblZ0WkhoZmRHRmliR1VnUEMwZ2JXRjBZMmhsWkY5aGJHd2dKVDRsWEc0Z0lITmxiR1ZqZENoZ1VHRnlkR2xqYVhCaGJuUWdTVVJnTENCY2JpQWdJQ0FnSUNBZ0lHQmpZWE5sWUN4Y2JpQWdJQ0FnSUNBZ0lHNTFiV1I0WDNaaGNpQTlJR0JPZFcxaVpYSWdiMllnYzJWc1ppMXlaWEJ2Y25SbFpDQnViMjR0WTJGdVkyVnlJR2xzYkc1bGMzTmxjeUI4SUVsdWMzUmhibU5sSURCZ0xGeHVJQ0FnSUNBZ0lDQWdJRzUxYlcxbFpITmZkbUZ5SUQwZ1lFNTFiV0psY2lCdlppQjBjbVZoZEcxbGJuUnpMMjFsWkdsallYUnBiMjV6SUhSaGEyVnVJSHdnU1c1emRHRnVZMlVnTUdBcFhHNWNibTUxYldSNFgzUmhZbXhsSUNVK0pWeHVJQ0JuY205MWNGOWllU2hqWVhObEtTQWxQaVZjYmlBZ2MzVnRiV0Z5YVhObEtGeHVJQ0FnSUc0Z1BTQnVLQ2tzWEc0Z0lDQWdiV1ZrYVdGdVgyNTFiV1I0SUQwZ2JXVmthV0Z1S0c1MWJXUjRYM1poY2l3Z2JtRXVjbTBnUFNCVVVsVkZLU3hjYmlBZ0lDQkpVVkpmYm5WdFpIZ2dQU0JKVVZJb2JuVnRaSGhmZG1GeUxDQnVZUzV5YlNBOUlGUlNWVVVwTEZ4dUlDQWdJRzFsWVc1ZmJuVnRaSGdnUFNCdFpXRnVLRzUxYldSNFgzWmhjaXdnYm1FdWNtMGdQU0JVVWxWRktTd2dJQ01nYW5WemRDQm1iM0lnWTI5dWRHVjRkRnh1SUNBZ0lITmtYMjUxYldSNElEMGdjMlFvYm5WdFpIaGZkbUZ5TENCdVlTNXliU0E5SUZSU1ZVVXBYRzRnSUNsY2JseHViblZ0WkhoZmRHRmliR1VnSlQ0bFhHNGdJR2R5YjNWd1gySjVLR05oYzJVcElDVStKVnh1SUNCemRXMXRZWEpwYzJVb1hHNGdJQ0FnYmlBOUlHNG9LU3hjYmlBZ0lDQnRaV1JwWVc1ZmJuVnRiV1ZrY3lBOUlHMWxaR2xoYmlodWRXMXRaV1J6WDNaaGNpd2dibUV1Y20wZ1BTQlVVbFZGS1N4Y2JpQWdJQ0JKVVZKZmJuVnRiV1ZrY3lBOUlFbFJVaWh1ZFcxdFpXUnpYM1poY2l3Z2JtRXVjbTBnUFNCVVVsVkZLU3hjYmlBZ0lDQnRaV0Z1WDI1MWJXMWxaSE1nUFNCdFpXRnVLRzUxYlcxbFpITmZkbUZ5TENCdVlTNXliU0E5SUZSU1ZVVXBMQ0FnSXlCcWRYTjBJR1p2Y2lCamIyNTBaWGgwWEc0Z0lDQWdjMlJmYm5WdGJXVmtjeUE5SUhOa0tHNTFiVzFsWkhOZmRtRnlMQ0J1WVM1eWJTQTlJRlJTVlVVcFhHNGdJQ2xjYmx4dWQybHNZMjk0TG5SbGMzUW9iblZ0WkhoZmRtRnlJSDRnWTJGelpTd2daR0YwWVNBOUlHNTFiV1I0WDNSaFlteGxLVnh1ZDJsc1kyOTRMblJsYzNRb2JuVnRiV1ZrYzE5MllYSWdmaUJqWVhObExDQmtZWFJoSUQwZ2JuVnRaSGhmZEdGaWJHVXBYRzVnWUdBaWZRPT0gLS0+XG5cbmBgYHJcbm51bWR4X3RhYmxlIDwtIG1hdGNoZWRfYWxsICU+JVxuICBzZWxlY3QoYFBhcnRpY2lwYW50IElEYCwgXG4gICAgICAgICBgY2FzZWAsXG4gICAgICAgICBudW1keF92YXIgPSBgTnVtYmVyIG9mIHNlbGYtcmVwb3J0ZWQgbm9uLWNhbmNlciBpbGxuZXNzZXMgfCBJbnN0YW5jZSAwYCxcbiAgICAgICAgICBudW1tZWRzX3ZhciA9IGBOdW1iZXIgb2YgdHJlYXRtZW50cy9tZWRpY2F0aW9ucyB0YWtlbiB8IEluc3RhbmNlIDBgKVxuXG5udW1keF90YWJsZSAlPiVcbiAgZ3JvdXBfYnkoY2FzZSkgJT4lXG4gIHN1bW1hcmlzZShcbiAgICBuID0gbigpLFxuICAgIG1lZGlhbl9udW1keCA9IG1lZGlhbihudW1keF92YXIsIG5hLnJtID0gVFJVRSksXG4gICAgSVFSX251bWR4ID0gSVFSKG51bWR4X3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBtZWFuX251bWR4ID0gbWVhbihudW1keF92YXIsIG5hLnJtID0gVFJVRSksICAjIGp1c3QgZm9yIGNvbnRleHRcbiAgICBzZF9udW1keCA9IHNkKG51bWR4X3ZhciwgbmEucm0gPSBUUlVFKVxuICApXG5cbm51bWR4X3RhYmxlICU+JVxuICBncm91cF9ieShjYXNlKSAlPiVcbiAgc3VtbWFyaXNlKFxuICAgIG4gPSBuKCksXG4gICAgbWVkaWFuX251bW1lZHMgPSBtZWRpYW4obnVtbWVkc192YXIsIG5hLnJtID0gVFJVRSksXG4gICAgSVFSX251bW1lZHMgPSBJUVIobnVtbWVkc192YXIsIG5hLnJtID0gVFJVRSksXG4gICAgbWVhbl9udW1tZWRzID0gbWVhbihudW1tZWRzX3ZhciwgbmEucm0gPSBUUlVFKSwgICMganVzdCBmb3IgY29udGV4dFxuICAgIHNkX251bW1lZHMgPSBzZChudW1tZWRzX3ZhciwgbmEucm0gPSBUUlVFKVxuICApXG5cbndpbGNveC50ZXN0KG51bWR4X3ZhciB+IGNhc2UsIGRhdGEgPSBudW1keF90YWJsZSlcbndpbGNveC50ZXN0KG51bW1lZHNfdmFyIH4gY2FzZSwgZGF0YSA9IG51bWR4X3RhYmxlKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubnVtZHhfdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgIG51bWR4X3ZhciA9IGBOdW1iZXIgb2Ygc2VsZi1yZXBvcnRlZCBub24tY2FuY2VyIGlsbG5lc3NlcyB8IEluc3RhbmNlIDBgLFxuICAgICAgICAgIG51bW1lZHNfdmFyID0gYE51bWJlciBvZiB0cmVhdG1lbnRzL21lZGljYXRpb25zIHRha2VuIHwgSW5zdGFuY2UgMGApXG5cbm51bWR4X3RhYmxlICU+JVxuICBncm91cF9ieShjYXNlKSAlPiVcbiAgc3VtbWFyaXNlKFxuICAgIG4gPSBuKCksXG4gICAgbWVkaWFuX251bWR4ID0gbWVkaWFuKG51bWR4X3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBJUVJfbnVtZHggPSBJUVIobnVtZHhfdmFyLCBuYS5ybSA9IFRSVUUpLFxuICAgIG1lYW5fbnVtZHggPSBtZWFuKG51bWR4X3ZhciwgbmEucm0gPSBUUlVFKSwgICMganVzdCBmb3IgY29udGV4dFxuICAgIHNkX251bWR4ID0gc2QobnVtZHhfdmFyLCBuYS5ybSA9IFRSVUUpXG4gIClcblxubnVtZHhfdGFibGUgJT4lXG4gIGdyb3VwX2J5KGNhc2UpICU+JVxuICBzdW1tYXJpc2UoXG4gICAgbiA9IG4oKSxcbiAgICBtZWRpYW5fbnVtbWVkcyA9IG1lZGlhbihudW1tZWRzX3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBJUVJfbnVtbWVkcyA9IElRUihudW1tZWRzX3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBtZWFuX251bW1lZHMgPSBtZWFuKG51bW1lZHNfdmFyLCBuYS5ybSA9IFRSVUUpLCAgIyBqdXN0IGZvciBjb250ZXh0XG4gICAgc2RfbnVtbWVkcyA9IHNkKG51bW1lZHNfdmFyLCBuYS5ybSA9IFRSVUUpXG4gIClcblxud2lsY294LnRlc3QobnVtZHhfdmFyIH4gY2FzZSwgZGF0YSA9IG51bWR4X3RhYmxlKVxud2lsY294LnRlc3QobnVtbWVkc192YXIgfiBjYXNlLCBkYXRhID0gbnVtZHhfdGFibGUpXG5gYGAifQ== -->

```r
numdx_table <- matched_all %>%
  select(`Participant ID`, 
         `case`,
         numdx_var = `Number of self-reported non-cancer illnesses | Instance 0`,
          nummeds_var = `Number of treatments/medications taken | Instance 0`)

numdx_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    median_numdx = median(numdx_var, na.rm = TRUE),
    IQR_numdx = IQR(numdx_var, na.rm = TRUE),
    mean_numdx = mean(numdx_var, na.rm = TRUE),  # just for context
    sd_numdx = sd(numdx_var, na.rm = TRUE)
  )

numdx_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    median_nummeds = median(nummeds_var, na.rm = TRUE),
    IQR_nummeds = IQR(nummeds_var, na.rm = TRUE),
    mean_nummeds = mean(nummeds_var, na.rm = TRUE),  # just for context
    sd_nummeds = sd(nummeds_var, na.rm = TRUE)
  )

wilcox.test(numdx_var ~ case, data = numdx_table)
wilcox.test(nummeds_var ~ case, data = numdx_table)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Analysis - education level (12 years as cutoff for higher education)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVaV1IxWDNSaFlteGxJRHd0SUcxaGRHTm9aV1JmWVd4c0lDVStKVnh1SUNCelpXeGxZM1FvWUZCaGNuUnBZMmx3WVc1MElFbEVZQ3dnWEc0Z0lDQWdJQ0FnSUNCZ1kyRnpaV0FzWEc0Z0lDQWdJQ0FnSUNBZ1pXUjFYM1poY2lBOUlHQlJkV0ZzYVdacFkyRjBhVzl1Y3lCOElFbHVjM1JoYm1ObElEQmdLU0FsUGlWY2JpQWdJQ0FnSUNBZ0lDQnRkWFJoZEdVb1hHNGdJQ0FnSUNBZ0lDQWdJQ0JvYVdkb1gyVmtkU0E5SUdOaGMyVmZkMmhsYmloY2JpQWdJQ0FnSUNBZ0lDQWdJQ0FnYzNSeVgyUmxkR1ZqZENobFpIVmZkbUZ5TENCY0lrTnZiR3hsWjJVZ2IzSWdWVzVwZG1WeWMybDBlU0JrWldkeVpXVmNJaWtnZmlBeFRDeGNiaUFnSUNBZ0lDQWdJQ0FnSUNBZ2MzUnlYMlJsZEdWamRDaGxaSFZmZG1GeUxDQmNJa0VnYkdWMlpXeHpMMEZUSUd4bGRtVnNjeUJ2Y2lCbGNYVnBkbUZzWlc1MFhDSXBJSDRnTVV3c1hHNGdJQ0FnSUNBZ0lDQWdJQ0FnSUhOMGNsOWtaWFJsWTNRb1pXUjFYM1poY2l3Z1hDSk9WbEVnYjNJZ1NFNUVJRzl5SUVoT1F5QnZjaUJsY1hWcGRtRnNaVzUwWENJcElINGdNVXdzWEc0Z0lDQWdJQ0FnSUNBZ0lDQWdJSE4wY2w5a1pYUmxZM1FvWldSMVgzWmhjaXdnWENKUGRHaGxjaUJ3Y205bVpYTnphVzl1WVd3Z2NYVmhiR2xtYVdOaGRHbHZibk5jSWlrZ2ZpQXhUQ3hjYmlBZ0lDQWdJQ0FnSUNBZ0lDQWdjM1J5WDJSbGRHVmpkQ2hsWkhWZmRtRnlMQ0JjSWs1dmJtVWdiMllnZEdobElHRmliM1psWENJcElINGdNRXdzWEc0Z0lDQWdJQ0FnSUNBZ0lDQWdJSE4wY2w5a1pYUmxZM1FvWldSMVgzWmhjaXdnWENKUWNtVm1aWElnYm05MElIUnZJR0Z1YzNkbGNsd2lLU0IrSUU1QlgybHVkR1ZuWlhKZkxGeHVJQ0FnSUNBZ0lDQWdJQ0FnSUNCVVVsVkZJSDRnTUV4Y2JpQWdJQ0FnSUNBZ0lDQWdJQ2xjYmlBZ0lDQWdJQ0FnSUNBcElDVStKVnh1SUNBZ0lHWnBiSFJsY2lnaGFYTXVibUVvYUdsbmFGOWxaSFVwS1Z4dVhHNGpJRk4xYlcxaGNtbDZaU0JqYjNWdWRITWdZVzVrSUhCbGNtTmxiblJoWjJWelhHNWxaSFZmYzNWdGJXRnllU0E4TFNCbFpIVmZkR0ZpYkdVZ0pUNGxYRzRnSUdkeWIzVndYMko1S0dOaGMyVXBJQ1UrSlZ4dUlDQnpkVzF0WVhKcGMyVW9YRzRnSUNBZ2JpQTlJRzRvS1N4Y2JpQWdJQ0J1WDJocFoyZ2dQU0J6ZFcwb2FHbG5hRjlsWkhVZ1BUMGdNU2tzWEc0Z0lDQWdjR1Z5WTJWdWRGOW9hV2RvSUQwZ01UQXdJQ29nYldWaGJpaG9hV2RvWDJWa2RTQTlQU0F4S1N4Y2JpQWdJQ0F1WjNKdmRYQnpJRDBnWENKa2NtOXdYQ0pjYmlBZ0tWeHVYRzV3Y21sdWRDaGxaSFZmYzNWdGJXRnllU2xjYmx4dUl5QXllRElnWTI5dWRHbHVaMlZ1WTNrZ2RHRmliR1ZjYm1Wa2RWOTBZV0lnUEMwZ2RHRmliR1VvWldSMVgzUmhZbXhsSkdOaGMyVXNJR1ZrZFY5MFlXSnNaU1JvYVdkb1gyVmtkU2xjYm1Wa2RWOTBZV0pjYmx4dUl5QkRhR2t0YzNGMVlYSmxJSFJsYzNRZ0tIZHZjbXR6SUdsbUlHVjRjR1ZqZEdWa0lHTnZkVzUwY3lBK1BTQTFLVnh1WTJocGMzRXVkR1Z6ZENobFpIVmZkR0ZpS1Z4dVlHQmdJbjA9IC0tPlxuXG5gYGByXG5lZHVfdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgICBlZHVfdmFyID0gYFF1YWxpZmljYXRpb25zIHwgSW5zdGFuY2UgMGApICU+JVxuICAgICAgICAgIG11dGF0ZShcbiAgICAgICAgICAgIGhpZ2hfZWR1ID0gY2FzZV93aGVuKFxuICAgICAgICAgICAgICBzdHJfZGV0ZWN0KGVkdV92YXIsIFwiQ29sbGVnZSBvciBVbml2ZXJzaXR5IGRlZ3JlZVwiKSB+IDFMLFxuICAgICAgICAgICAgICBzdHJfZGV0ZWN0KGVkdV92YXIsIFwiQSBsZXZlbHMvQVMgbGV2ZWxzIG9yIGVxdWl2YWxlbnRcIikgfiAxTCxcbiAgICAgICAgICAgICAgc3RyX2RldGVjdChlZHVfdmFyLCBcIk5WUSBvciBITkQgb3IgSE5DIG9yIGVxdWl2YWxlbnRcIikgfiAxTCxcbiAgICAgICAgICAgICAgc3RyX2RldGVjdChlZHVfdmFyLCBcIk90aGVyIHByb2Zlc3Npb25hbCBxdWFsaWZpY2F0aW9uc1wiKSB+IDFMLFxuICAgICAgICAgICAgICBzdHJfZGV0ZWN0KGVkdV92YXIsIFwiTm9uZSBvZiB0aGUgYWJvdmVcIikgfiAwTCxcbiAgICAgICAgICAgICAgc3RyX2RldGVjdChlZHVfdmFyLCBcIlByZWZlciBub3QgdG8gYW5zd2VyXCIpIH4gTkFfaW50ZWdlcl8sXG4gICAgICAgICAgICAgIFRSVUUgfiAwTFxuICAgICAgICAgICAgKVxuICAgICAgICAgICkgJT4lXG4gICAgZmlsdGVyKCFpcy5uYShoaWdoX2VkdSkpXG5cbiMgU3VtbWFyaXplIGNvdW50cyBhbmQgcGVyY2VudGFnZXNcbmVkdV9zdW1tYXJ5IDwtIGVkdV90YWJsZSAlPiVcbiAgZ3JvdXBfYnkoY2FzZSkgJT4lXG4gIHN1bW1hcmlzZShcbiAgICBuID0gbigpLFxuICAgIG5faGlnaCA9IHN1bShoaWdoX2VkdSA9PSAxKSxcbiAgICBwZXJjZW50X2hpZ2ggPSAxMDAgKiBtZWFuKGhpZ2hfZWR1ID09IDEpLFxuICAgIC5ncm91cHMgPSBcImRyb3BcIlxuICApXG5cbnByaW50KGVkdV9zdW1tYXJ5KVxuXG4jIDJ4MiBjb250aW5nZW5jeSB0YWJsZVxuZWR1X3RhYiA8LSB0YWJsZShlZHVfdGFibGUkY2FzZSwgZWR1X3RhYmxlJGhpZ2hfZWR1KVxuZWR1X3RhYlxuXG4jIENoaS1zcXVhcmUgdGVzdCAod29ya3MgaWYgZXhwZWN0ZWQgY291bnRzID49IDUpXG5jaGlzcS50ZXN0KGVkdV90YWIpXG5gYGBcblxuPCEtLSBybmItc291cmNlLWVuZCAtLT5cbiJ9 -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZWR1X3RhYmxlIDwtIG1hdGNoZWRfYWxsICU+JVxuICBzZWxlY3QoYFBhcnRpY2lwYW50IElEYCwgXG4gICAgICAgICBgY2FzZWAsXG4gICAgICAgICAgZWR1X3ZhciA9IGBRdWFsaWZpY2F0aW9ucyB8IEluc3RhbmNlIDBgKSAlPiVcbiAgICAgICAgICBtdXRhdGUoXG4gICAgICAgICAgICBoaWdoX2VkdSA9IGNhc2Vfd2hlbihcbiAgICAgICAgICAgICAgc3RyX2RldGVjdChlZHVfdmFyLCBcIkNvbGxlZ2Ugb3IgVW5pdmVyc2l0eSBkZWdyZWVcIikgfiAxTCxcbiAgICAgICAgICAgICAgc3RyX2RldGVjdChlZHVfdmFyLCBcIkEgbGV2ZWxzL0FTIGxldmVscyBvciBlcXVpdmFsZW50XCIpIH4gMUwsXG4gICAgICAgICAgICAgIHN0cl9kZXRlY3QoZWR1X3ZhciwgXCJOVlEgb3IgSE5EIG9yIEhOQyBvciBlcXVpdmFsZW50XCIpIH4gMUwsXG4gICAgICAgICAgICAgIHN0cl9kZXRlY3QoZWR1X3ZhciwgXCJPdGhlciBwcm9mZXNzaW9uYWwgcXVhbGlmaWNhdGlvbnNcIikgfiAxTCxcbiAgICAgICAgICAgICAgc3RyX2RldGVjdChlZHVfdmFyLCBcIk5vbmUgb2YgdGhlIGFib3ZlXCIpIH4gMEwsXG4gICAgICAgICAgICAgIHN0cl9kZXRlY3QoZWR1X3ZhciwgXCJQcmVmZXIgbm90IHRvIGFuc3dlclwiKSB+IE5BX2ludGVnZXJfLFxuICAgICAgICAgICAgICBUUlVFIH4gMExcbiAgICAgICAgICAgIClcbiAgICAgICAgICApICU+JVxuICAgIGZpbHRlcighaXMubmEoaGlnaF9lZHUpKVxuXG4jIFN1bW1hcml6ZSBjb3VudHMgYW5kIHBlcmNlbnRhZ2VzXG5lZHVfc3VtbWFyeSA8LSBlZHVfdGFibGUgJT4lXG4gIGdyb3VwX2J5KGNhc2UpICU+JVxuICBzdW1tYXJpc2UoXG4gICAgbiA9IG4oKSxcbiAgICBuX2hpZ2ggPSBzdW0oaGlnaF9lZHUgPT0gMSksXG4gICAgcGVyY2VudF9oaWdoID0gMTAwICogbWVhbihoaWdoX2VkdSA9PSAxKSxcbiAgICAuZ3JvdXBzID0gXCJkcm9wXCJcbiAgKVxuXG5wcmludChlZHVfc3VtbWFyeSlcblxuIyAyeDIgY29udGluZ2VuY3kgdGFibGVcbmVkdV90YWIgPC0gdGFibGUoZWR1X3RhYmxlJGNhc2UsIGVkdV90YWJsZSRoaWdoX2VkdSlcbmVkdV90YWJcblxuIyBDaGktc3F1YXJlIHRlc3QgKHdvcmtzIGlmIGV4cGVjdGVkIGNvdW50cyA+PSA1KVxuY2hpc3EudGVzdChlZHVfdGFiKVxuYGBgIn0= -->

```r
edu_table <- matched_all %>%
  select(`Participant ID`, 
         `case`,
          edu_var = `Qualifications | Instance 0`) %>%
          mutate(
            high_edu = case_when(
              str_detect(edu_var, "College or University degree") ~ 1L,
              str_detect(edu_var, "A levels/AS levels or equivalent") ~ 1L,
              str_detect(edu_var, "NVQ or HND or HNC or equivalent") ~ 1L,
              str_detect(edu_var, "Other professional qualifications") ~ 1L,
              str_detect(edu_var, "None of the above") ~ 0L,
              str_detect(edu_var, "Prefer not to answer") ~ NA_integer_,
              TRUE ~ 0L
            )
          ) %>%
    filter(!is.na(high_edu))

# Summarize counts and percentages
edu_summary <- edu_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    n_high = sum(high_edu == 1),
    percent_high = 100 * mean(high_edu == 1),
    .groups = "drop"
  )

print(edu_summary)

# 2x2 contingency table
edu_tab <- table(edu_table$case, edu_table$high_edu)
edu_tab

# Chi-square test (works if expected counts >= 5)
chisq.test(edu_tab)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Analysis - smoking (based on pack-years only)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVjMjF2YTJsdVoxOTBZV0pzWlNBOExTQnRZWFJqYUdWa1gyRnNiQ0FsUGlWY2JpQWdjMlZzWldOMEtHQlFZWEowYVdOcGNHRnVkQ0JKUkdBc0lGeHVJQ0FnSUNBZ0lDQWdZR05oYzJWZ0xGeHVJQ0FnSUNBZ0lDQWdjR0ZqYTNseWMxOTJZWElnUFNCZ1VHRmpheUI1WldGeWN5QnZaaUJ6Ylc5cmFXNW5JSHdnU1c1emRHRnVZMlVnTUdBcElDVStKVnh1SUNCdGRYUmhkR1VvY0dGamEzbHljMTkyWVhJZ1BTQnlaWEJzWVdObFgyNWhLSEJoWTJ0NWNuTmZkbUZ5TENBd0tTa2dKVDRsWEc0Z0lHMTFkR0YwWlNodVpYWmxjbDl6Ylc5clpYSWdQU0JwWmw5bGJITmxLSEJoWTJ0NWNuTmZkbUZ5SUQwOUlEQXNJREZNTENBd1RDa3BYRzVjYm5OdGIydHBibWRmZEdGaWJHVWdKVDRsWEc0Z0lHZHliM1Z3WDJKNUtHTmhjMlVwSUNVK0pWeHVJQ0J6ZFcxdFlYSnBjMlVvWEc0Z0lDQWdiaUE5SUc0b0tTeGNiaUFnSUNCdFpXUnBZVzVmY0dGamEzbHljeUE5SUcxbFpHbGhiaWh3WVdOcmVYSnpYM1poY2l3Z2JtRXVjbTBnUFNCVVVsVkZLU3hjYmlBZ0lDQkpVVkpmY0dGamEzbHljeUE5SUVsUlVpaHdZV05yZVhKelgzWmhjaXdnYm1FdWNtMGdQU0JVVWxWRktTeGNiaUFnSUNCdFpXRnVYM0JoWTJ0NWNuTWdQU0J0WldGdUtIQmhZMnQ1Y25OZmRtRnlMQ0J1WVM1eWJTQTlJRlJTVlVVcExDQWdJeUJxZFhOMElHWnZjaUJqYjI1MFpYaDBYRzRnSUNBZ2MyUmZjR0ZqYTNseWN5QTlJSE5rS0hCaFkydDVjbk5mZG1GeUxDQnVZUzV5YlNBOUlGUlNWVVVwWEc0Z0lDbGNibHh1SXlCVGRXMXRZWEpwZW1VZ2NHVnlZMlZ1ZEdGblpYTWdZbmtnWTJGelpTQnpkR0YwZFhOY2JuTnRiMnRwYm1kZmMzVnRiV0Z5ZVNBOExTQnpiVzlyYVc1blgzUmhZbXhsSUNVK0pWeHVJQ0JuY205MWNGOWllU2hqWVhObEtTQWxQaVZjYmlBZ2MzVnRiV0Z5YVhObEtGeHVJQ0FnSUc0Z1BTQnVLQ2tzWEc0Z0lDQWdibDl1WlhabGNpQTlJSE4xYlNodVpYWmxjbDl6Ylc5clpYSXBMRnh1SUNBZ0lIQmxjbU5sYm5SZmJtVjJaWElnUFNBeE1EQWdLaUJ0WldGdUtHNWxkbVZ5WDNOdGIydGxjaWtzWEc0Z0lDQWdMbWR5YjNWd2N5QTlJRndpWkhKdmNGd2lYRzRnSUNsY2JseHVjSEpwYm5Rb2MyMXZhMmx1WjE5emRXMXRZWEo1S1Z4dVhHNGpJREo0TWlCamIyNTBhVzVuWlc1amVTQjBZV0pzWlZ4dWMyMXZhMmx1WjE5MFlXSWdQQzBnZEdGaWJHVW9jMjF2YTJsdVoxOTBZV0pzWlNSallYTmxMQ0J6Ylc5cmFXNW5YM1JoWW14bEpHNWxkbVZ5WDNOdGIydGxjaWxjYm5OdGIydHBibWRmZEdGaVhHNWNiaU1nVTNSaGRHbHpkR2xqWVd3Z2RHVnpkRnh1ZDJsc1kyOTRMblJsYzNRb2NHRmphM2x5YzE5MllYSWdmaUJqWVhObExDQmtZWFJoSUQwZ2MyMXZhMmx1WjE5MFlXSnNaU2xjYm1Ob2FYTnhMblJsYzNRb2MyMXZhMmx1WjE5MFlXSXBYRzVnWUdBaWZRPT0gLS0+XG5cbmBgYHJcbnNtb2tpbmdfdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgIHBhY2t5cnNfdmFyID0gYFBhY2sgeWVhcnMgb2Ygc21va2luZyB8IEluc3RhbmNlIDBgKSAlPiVcbiAgbXV0YXRlKHBhY2t5cnNfdmFyID0gcmVwbGFjZV9uYShwYWNreXJzX3ZhciwgMCkpICU+JVxuICBtdXRhdGUobmV2ZXJfc21va2VyID0gaWZfZWxzZShwYWNreXJzX3ZhciA9PSAwLCAxTCwgMEwpKVxuXG5zbW9raW5nX3RhYmxlICU+JVxuICBncm91cF9ieShjYXNlKSAlPiVcbiAgc3VtbWFyaXNlKFxuICAgIG4gPSBuKCksXG4gICAgbWVkaWFuX3BhY2t5cnMgPSBtZWRpYW4ocGFja3lyc192YXIsIG5hLnJtID0gVFJVRSksXG4gICAgSVFSX3BhY2t5cnMgPSBJUVIocGFja3lyc192YXIsIG5hLnJtID0gVFJVRSksXG4gICAgbWVhbl9wYWNreXJzID0gbWVhbihwYWNreXJzX3ZhciwgbmEucm0gPSBUUlVFKSwgICMganVzdCBmb3IgY29udGV4dFxuICAgIHNkX3BhY2t5cnMgPSBzZChwYWNreXJzX3ZhciwgbmEucm0gPSBUUlVFKVxuICApXG5cbiMgU3VtbWFyaXplIHBlcmNlbnRhZ2VzIGJ5IGNhc2Ugc3RhdHVzXG5zbW9raW5nX3N1bW1hcnkgPC0gc21va2luZ190YWJsZSAlPiVcbiAgZ3JvdXBfYnkoY2FzZSkgJT4lXG4gIHN1bW1hcmlzZShcbiAgICBuID0gbigpLFxuICAgIG5fbmV2ZXIgPSBzdW0obmV2ZXJfc21va2VyKSxcbiAgICBwZXJjZW50X25ldmVyID0gMTAwICogbWVhbihuZXZlcl9zbW9rZXIpLFxuICAgIC5ncm91cHMgPSBcImRyb3BcIlxuICApXG5cbnByaW50KHNtb2tpbmdfc3VtbWFyeSlcblxuIyAyeDIgY29udGluZ2VuY3kgdGFibGVcbnNtb2tpbmdfdGFiIDwtIHRhYmxlKHNtb2tpbmdfdGFibGUkY2FzZSwgc21va2luZ190YWJsZSRuZXZlcl9zbW9rZXIpXG5zbW9raW5nX3RhYlxuXG4jIFN0YXRpc3RpY2FsIHRlc3RcbndpbGNveC50ZXN0KHBhY2t5cnNfdmFyIH4gY2FzZSwgZGF0YSA9IHNtb2tpbmdfdGFibGUpXG5jaGlzcS50ZXN0KHNtb2tpbmdfdGFiKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc21va2luZ190YWJsZSA8LSBtYXRjaGVkX2FsbCAlPiVcbiAgc2VsZWN0KGBQYXJ0aWNpcGFudCBJRGAsIFxuICAgICAgICAgYGNhc2VgLFxuICAgICAgICAgcGFja3lyc192YXIgPSBgUGFjayB5ZWFycyBvZiBzbW9raW5nIHwgSW5zdGFuY2UgMGApICU+JVxuICBtdXRhdGUocGFja3lyc192YXIgPSByZXBsYWNlX25hKHBhY2t5cnNfdmFyLCAwKSkgJT4lXG4gIG11dGF0ZShuZXZlcl9zbW9rZXIgPSBpZl9lbHNlKHBhY2t5cnNfdmFyID09IDAsIDFMLCAwTCkpXG5cbnNtb2tpbmdfdGFibGUgJT4lXG4gIGdyb3VwX2J5KGNhc2UpICU+JVxuICBzdW1tYXJpc2UoXG4gICAgbiA9IG4oKSxcbiAgICBtZWRpYW5fcGFja3lycyA9IG1lZGlhbihwYWNreXJzX3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBJUVJfcGFja3lycyA9IElRUihwYWNreXJzX3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBtZWFuX3BhY2t5cnMgPSBtZWFuKHBhY2t5cnNfdmFyLCBuYS5ybSA9IFRSVUUpLCAgIyBqdXN0IGZvciBjb250ZXh0XG4gICAgc2RfcGFja3lycyA9IHNkKHBhY2t5cnNfdmFyLCBuYS5ybSA9IFRSVUUpXG4gIClcblxuIyBTdW1tYXJpemUgcGVyY2VudGFnZXMgYnkgY2FzZSBzdGF0dXNcbnNtb2tpbmdfc3VtbWFyeSA8LSBzbW9raW5nX3RhYmxlICU+JVxuICBncm91cF9ieShjYXNlKSAlPiVcbiAgc3VtbWFyaXNlKFxuICAgIG4gPSBuKCksXG4gICAgbl9uZXZlciA9IHN1bShuZXZlcl9zbW9rZXIpLFxuICAgIHBlcmNlbnRfbmV2ZXIgPSAxMDAgKiBtZWFuKG5ldmVyX3Ntb2tlciksXG4gICAgLmdyb3VwcyA9IFwiZHJvcFwiXG4gIClcblxucHJpbnQoc21va2luZ19zdW1tYXJ5KVxuXG4jIDJ4MiBjb250aW5nZW5jeSB0YWJsZVxuc21va2luZ190YWIgPC0gdGFibGUoc21va2luZ190YWJsZSRjYXNlLCBzbW9raW5nX3RhYmxlJG5ldmVyX3Ntb2tlcilcbnNtb2tpbmdfdGFiXG5cbiMgU3RhdGlzdGljYWwgdGVzdFxud2lsY294LnRlc3QocGFja3lyc192YXIgfiBjYXNlLCBkYXRhID0gc21va2luZ190YWJsZSlcbmNoaXNxLnRlc3Qoc21va2luZ190YWIpXG5gYGAifQ== -->

```r
smoking_table <- matched_all %>%
  select(`Participant ID`, 
         `case`,
         packyrs_var = `Pack years of smoking | Instance 0`) %>%
  mutate(packyrs_var = replace_na(packyrs_var, 0)) %>%
  mutate(never_smoker = if_else(packyrs_var == 0, 1L, 0L))

smoking_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    median_packyrs = median(packyrs_var, na.rm = TRUE),
    IQR_packyrs = IQR(packyrs_var, na.rm = TRUE),
    mean_packyrs = mean(packyrs_var, na.rm = TRUE),  # just for context
    sd_packyrs = sd(packyrs_var, na.rm = TRUE)
  )

# Summarize percentages by case status
smoking_summary <- smoking_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    n_never = sum(never_smoker),
    percent_never = 100 * mean(never_smoker),
    .groups = "drop"
  )

print(smoking_summary)

# 2x2 contingency table
smoking_tab <- table(smoking_table$case, smoking_table$never_smoker)
smoking_tab

# Statistical test
wilcox.test(packyrs_var ~ case, data = smoking_table)
chisq.test(smoking_tab)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Import GP records

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVRMVJXWDJ4cFluSmhjbmtnUEMwZ2NtVmhaQzVrWW1Zb1hDSkRPaTlWYzJWeWN5OURhR0Z5YkdsbElGcG9ZVzh2VDI1bFJISnBkbVVnTFNCTllYTnpJRWRsYm1WeVlXd2dRbkpwWjJoaGJTOVNaWE5sWVhKamFDOVZTeUJDYVc5aVlXNXJMMjVvYzE5eVpXRmtZbkp2ZDNObGNsOHlOUzR3TGpCZk1qQXhPREEwTURFd01EQXdNREV2VTNSaGJtUmhjbVF2VmpNdlZHVnliUzVrWW1aY0lpbGNia05VVmw5MFpXMXdZVzVqWlNBOExTQnlaV0ZrTG1SaVppaGNJa002TDFWelpYSnpMME5vWVhKc2FXVWdXbWhoYnk5UGJtVkVjbWwyWlNBdElFMWhjM01nUjJWdVpYSmhiQ0JDY21sbmFHRnRMMUpsYzJWaGNtTm9MMVZMSUVKcGIySmhibXN2Ym1oelgzSmxZV1JpY205M2MyVnlYekkxTGpBdU1GOHlNREU0TURRd01UQXdNREF3TVM5VGRHRnVaR0Z5WkM5V015OVVSVTFRUVU1RFJTNWtZbVpjSWlsY2JrTlVWbDloYm1ObGMzUnZjaUE4TFNCeVpXRmtMbVJpWmloY0lrTTZMMVZ6WlhKekwwTm9ZWEpzYVdVZ1dtaGhieTlQYm1WRWNtbDJaU0F0SUUxaGMzTWdSMlZ1WlhKaGJDQkNjbWxuYUdGdEwxSmxjMlZoY21Ob0wxVkxJRUpwYjJKaGJtc3ZibWh6WDNKbFlXUmljbTkzYzJWeVh6STFMakF1TUY4eU1ERTRNRFF3TVRBd01EQXdNUzlUZEdGdVpHRnlaQzlXTXk5QlRrTkZVMVJQVWk1a1ltWmNJaWxjYmtOVVZsOW9hV1Z5SUR3dElISmxZV1F1WkdKbUtGd2lRem92VlhObGNuTXZRMmhoY214cFpTQmFhR0Z2TDA5dVpVUnlhWFpsSUMwZ1RXRnpjeUJIWlc1bGNtRnNJRUp5YVdkb1lXMHZVbVZ6WldGeVkyZ3ZWVXNnUW1sdlltRnVheTl1YUhOZmNtVmhaR0p5YjNkelpYSmZNalV1TUM0d1h6SXdNVGd3TkRBeE1EQXdNREF4TDFOMFlXNWtZWEprTDFZekwwaEpSVkl1WkdKbVhDSXBYRzVEVkZaZmRHVnRjR2hwWlhJZ1BDMGdjbVZoWkM1a1ltWW9YQ0pET2k5VmMyVnljeTlEYUdGeWJHbGxJRnBvWVc4dlQyNWxSSEpwZG1VZ0xTQk5ZWE56SUVkbGJtVnlZV3dnUW5KcFoyaGhiUzlTWlhObFlYSmphQzlWU3lCQ2FXOWlZVzVyTDI1b2MxOXlaV0ZrWW5KdmQzTmxjbDh5TlM0d0xqQmZNakF4T0RBME1ERXdNREF3TURFdlUzUmhibVJoY21RdlZqTXZWRVZOVUVoSlJWSXVaR0ptWENJcFhHNURWRlpmWTI5dVkyVndkQ0E4TFNCeVpXRmtMbVJpWmloY0lrTTZMMVZ6WlhKekwwTm9ZWEpzYVdVZ1dtaGhieTlQYm1WRWNtbDJaU0F0SUUxaGMzTWdSMlZ1WlhKaGJDQkNjbWxuYUdGdEwxSmxjMlZoY21Ob0wxVkxJRUpwYjJKaGJtc3ZibWh6WDNKbFlXUmljbTkzYzJWeVh6STFMakF1TUY4eU1ERTRNRFF3TVRBd01EQXdNUzlUZEdGdVpHRnlaQzlXTXk5RFQwNURSVkJVTG1SaVpsd2lLVnh1UTFSV1gzUmxjbTB4T1RnZ1BDMGdjbVZoWkM1a1ltWW9YQ0pET2k5VmMyVnljeTlEYUdGeWJHbGxJRnBvWVc4dlQyNWxSSEpwZG1VZ0xTQk5ZWE56SUVkbGJtVnlZV3dnUW5KcFoyaGhiUzlTWlhObFlYSmphQzlWU3lCQ2FXOWlZVzVyTDI1b2MxOXlaV0ZrWW5KdmQzTmxjbDh5TlM0d0xqQmZNakF4T0RBME1ERXdNREF3TURFdlUzUmhibVJoY21RdlZqTXZWRVZTVFRFNU9DNWtZbVpjSWlsY2JrTlVWbDlKUTBReE1DQThMU0J5WldGa0xtUmlaaWhjSWtNNkwxVnpaWEp6TDBOb1lYSnNhV1VnV21oaGJ5OVBibVZFY21sMlpTQXRJRTFoYzNNZ1IyVnVaWEpoYkNCQ2NtbG5hR0Z0TDFKbGMyVmhjbU5vTDFWTElFSnBiMkpoYm1zdmJtaHpYM0psWVdSaWNtOTNjMlZ5WHpJMUxqQXVNRjh5TURFNE1EUXdNVEF3TURBd01TOVRkR0Z1WkdGeVpDOVdNeTlKUTBReE1DNWtZbVpjSWlsY2JrTlVWbDlEYjIxd2EyVjVJRHd0SUhKbFlXUXVaR0ptS0Z3aVF6b3ZWWE5sY25NdlEyaGhjbXhwWlNCYWFHRnZMMDl1WlVSeWFYWmxJQzBnVFdGemN5QkhaVzVsY21Gc0lFSnlhV2RvWVcwdlVtVnpaV0Z5WTJndlZVc2dRbWx2WW1GdWF5OXVhSE5mY21WaFpHSnliM2R6WlhKZk1qVXVNQzR3WHpJd01UZ3dOREF4TURBd01EQXhMMU4wWVc1a1lYSmtMMVl6TDBOUFRWQkxSVmswTG1SaVpsd2lLVnh1WEc1Y2JsQlRVRjlIVUd4bGRtVnNJRHd0SUhKbFlXUmZZM04yS0Z3aVF6b3ZWWE5sY25NdlEyaGhjbXhwWlNCYWFHRnZMMDl1WlVSeWFYWmxJQzBnVFdGemN5QkhaVzVsY21Gc0lFSnlhV2RvWVcwdlVtVnpaV0Z5WTJndlZVc2dRbWx2WW1GdWF5OUVZWFJoTDFCVFVDMTNMVWRRTFc5dWJIbGZSMUJzWlhabGJDNWpjM1pjSWlsY2JseHVZR0JnSW4wPSAtLT5cblxuYGBgclxuQ1RWX2xpYnJhcnkgPC0gcmVhZC5kYmYoXCJDOi9Vc2Vycy9DaGFybGllIFpoYW8vT25lRHJpdmUgLSBNYXNzIEdlbmVyYWwgQnJpZ2hhbS9SZXNlYXJjaC9VSyBCaW9iYW5rL25oc19yZWFkYnJvd3Nlcl8yNS4wLjBfMjAxODA0MDEwMDAwMDEvU3RhbmRhcmQvVjMvVGVybS5kYmZcIilcbkNUVl90ZW1wYW5jZSA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9URU1QQU5DRS5kYmZcIilcbkNUVl9hbmNlc3RvciA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9BTkNFU1RPUi5kYmZcIilcbkNUVl9oaWVyIDwtIHJlYWQuZGJmKFwiQzovVXNlcnMvQ2hhcmxpZSBaaGFvL09uZURyaXZlIC0gTWFzcyBHZW5lcmFsIEJyaWdoYW0vUmVzZWFyY2gvVUsgQmlvYmFuay9uaHNfcmVhZGJyb3dzZXJfMjUuMC4wXzIwMTgwNDAxMDAwMDAxL1N0YW5kYXJkL1YzL0hJRVIuZGJmXCIpXG5DVFZfdGVtcGhpZXIgPC0gcmVhZC5kYmYoXCJDOi9Vc2Vycy9DaGFybGllIFpoYW8vT25lRHJpdmUgLSBNYXNzIEdlbmVyYWwgQnJpZ2hhbS9SZXNlYXJjaC9VSyBCaW9iYW5rL25oc19yZWFkYnJvd3Nlcl8yNS4wLjBfMjAxODA0MDEwMDAwMDEvU3RhbmRhcmQvVjMvVEVNUEhJRVIuZGJmXCIpXG5DVFZfY29uY2VwdCA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9DT05DRVBULmRiZlwiKVxuQ1RWX3Rlcm0xOTggPC0gcmVhZC5kYmYoXCJDOi9Vc2Vycy9DaGFybGllIFpoYW8vT25lRHJpdmUgLSBNYXNzIEdlbmVyYWwgQnJpZ2hhbS9SZXNlYXJjaC9VSyBCaW9iYW5rL25oc19yZWFkYnJvd3Nlcl8yNS4wLjBfMjAxODA0MDEwMDAwMDEvU3RhbmRhcmQvVjMvVEVSTTE5OC5kYmZcIilcbkNUVl9JQ0QxMCA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9JQ0QxMC5kYmZcIilcbkNUVl9Db21wa2V5IDwtIHJlYWQuZGJmKFwiQzovVXNlcnMvQ2hhcmxpZSBaaGFvL09uZURyaXZlIC0gTWFzcyBHZW5lcmFsIEJyaWdoYW0vUmVzZWFyY2gvVUsgQmlvYmFuay9uaHNfcmVhZGJyb3dzZXJfMjUuMC4wXzIwMTgwNDAxMDAwMDAxL1N0YW5kYXJkL1YzL0NPTVBLRVk0LmRiZlwiKVxuXG5cblBTUF9HUGxldmVsIDwtIHJlYWRfY3N2KFwiQzovVXNlcnMvQ2hhcmxpZSBaaGFvL09uZURyaXZlIC0gTWFzcyBHZW5lcmFsIEJyaWdoYW0vUmVzZWFyY2gvVUsgQmlvYmFuay9EYXRhL1BTUC13LUdQLW9ubHlfR1BsZXZlbC5jc3ZcIilcblxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuQ1RWX2xpYnJhcnkgPC0gcmVhZC5kYmYoXCJDOi9Vc2Vycy9DaGFybGllIFpoYW8vT25lRHJpdmUgLSBNYXNzIEdlbmVyYWwgQnJpZ2hhbS9SZXNlYXJjaC9VSyBCaW9iYW5rL25oc19yZWFkYnJvd3Nlcl8yNS4wLjBfMjAxODA0MDEwMDAwMDEvU3RhbmRhcmQvVjMvVGVybS5kYmZcIilcbkNUVl90ZW1wYW5jZSA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9URU1QQU5DRS5kYmZcIilcbkNUVl9hbmNlc3RvciA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9BTkNFU1RPUi5kYmZcIilcbkNUVl9oaWVyIDwtIHJlYWQuZGJmKFwiQzovVXNlcnMvQ2hhcmxpZSBaaGFvL09uZURyaXZlIC0gTWFzcyBHZW5lcmFsIEJyaWdoYW0vUmVzZWFyY2gvVUsgQmlvYmFuay9uaHNfcmVhZGJyb3dzZXJfMjUuMC4wXzIwMTgwNDAxMDAwMDAxL1N0YW5kYXJkL1YzL0hJRVIuZGJmXCIpXG5DVFZfdGVtcGhpZXIgPC0gcmVhZC5kYmYoXCJDOi9Vc2Vycy9DaGFybGllIFpoYW8vT25lRHJpdmUgLSBNYXNzIEdlbmVyYWwgQnJpZ2hhbS9SZXNlYXJjaC9VSyBCaW9iYW5rL25oc19yZWFkYnJvd3Nlcl8yNS4wLjBfMjAxODA0MDEwMDAwMDEvU3RhbmRhcmQvVjMvVEVNUEhJRVIuZGJmXCIpXG5DVFZfY29uY2VwdCA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9DT05DRVBULmRiZlwiKVxuQ1RWX3Rlcm0xOTggPC0gcmVhZC5kYmYoXCJDOi9Vc2Vycy9DaGFybGllIFpoYW8vT25lRHJpdmUgLSBNYXNzIEdlbmVyYWwgQnJpZ2hhbS9SZXNlYXJjaC9VSyBCaW9iYW5rL25oc19yZWFkYnJvd3Nlcl8yNS4wLjBfMjAxODA0MDEwMDAwMDEvU3RhbmRhcmQvVjMvVEVSTTE5OC5kYmZcIilcbkNUVl9JQ0QxMCA8LSByZWFkLmRiZihcIkM6L1VzZXJzL0NoYXJsaWUgWmhhby9PbmVEcml2ZSAtIE1hc3MgR2VuZXJhbCBCcmlnaGFtL1Jlc2VhcmNoL1VLIEJpb2JhbmsvbmhzX3JlYWRicm93c2VyXzI1LjAuMF8yMDE4MDQwMTAwMDAwMS9TdGFuZGFyZC9WMy9JQ0QxMC5kYmZcIilcbkNUVl9Db21wa2V5IDwtIHJlYWQuZGJmKFwiQzovVXNlcnMvQ2hhcmxpZSBaaGFvL09uZURyaXZlIC0gTWFzcyBHZW5lcmFsIEJyaWdoYW0vUmVzZWFyY2gvVUsgQmlvYmFuay9uaHNfcmVhZGJyb3dzZXJfMjUuMC4wXzIwMTgwNDAxMDAwMDAxL1N0YW5kYXJkL1YzL0NPTVBLRVk0LmRiZlwiKVxuXG5cblBTUF9HUGxldmVsIDwtIHJlYWRfY3N2KFwiQzovVXNlcnMvQ2hhcmxpZSBaaGFvL09uZURyaXZlIC0gTWFzcyBHZW5lcmFsIEJyaWdoYW0vUmVzZWFyY2gvVUsgQmlvYmFuay9EYXRhL1BTUC13LUdQLW9ubHlfR1BsZXZlbC5jc3ZcIilcblxuYGBgIn0= -->

```r
CTV_library <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/Term.dbf")
CTV_tempance <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/TEMPANCE.dbf")
CTV_ancestor <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/ANCESTOR.dbf")
CTV_hier <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/HIER.dbf")
CTV_temphier <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/TEMPHIER.dbf")
CTV_concept <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/CONCEPT.dbf")
CTV_term198 <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/TERM198.dbf")
CTV_ICD10 <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/ICD10.dbf")
CTV_Compkey <- read.dbf("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/nhs_readbrowser_25.0.0_20180401000001/Standard/V3/COMPKEY4.dbf")


PSP_GPlevel <- read_csv("C:/Users/Charlie Zhao/OneDrive - Mass General Brigham/Research/UK Biobank/Data/PSP-w-GP-only_GPlevel.csv")

```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Join

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVVRk5RWDBkUWJHVjJaV3dnUEMwZ1VGTlFYMGRRYkdWMlpXd2dKVDRsWEc0Z0lHeGxablJmYW05cGJpaGNiaUFnSUNCRFZGWmZiR2xpY21GeWVTQWxQaVVnYzJWc1pXTjBLRlJGVWsxSlJDd2dWRVZTVFRNd0tTeGNiaUFnSUNCaWVTQTlJR01vWENKRFZGWXpJQ2hTWldGa0lIWXpLU0JqYjJSbFhDSWdQU0JjSWxSRlVrMUpSRndpS1Z4dUlDQXBJQ1UrSlZ4dUlDQnlaVzVoYldVb1ZHVnliU0E5SUZSRlVrMHpNQ2xjYm1CZ1lDSjkgLS0+XG5cbmBgYHJcblBTUF9HUGxldmVsIDwtIFBTUF9HUGxldmVsICU+JVxuICBsZWZ0X2pvaW4oXG4gICAgQ1RWX2xpYnJhcnkgJT4lIHNlbGVjdChURVJNSUQsIFRFUk0zMCksXG4gICAgYnkgPSBjKFwiQ1RWMyAoUmVhZCB2MykgY29kZVwiID0gXCJURVJNSURcIilcbiAgKSAlPiVcbiAgcmVuYW1lKFRlcm0gPSBURVJNMzApXG5gYGBcblxuPCEtLSBybmItc291cmNlLWVuZCAtLT5cbiJ9 -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuUFNQX0dQbGV2ZWwgPC0gUFNQX0dQbGV2ZWwgJT4lXG4gIGxlZnRfam9pbihcbiAgICBDVFZfbGlicmFyeSAlPiUgc2VsZWN0KFRFUk1JRCwgVEVSTTMwKSxcbiAgICBieSA9IGMoXCJDVFYzIChSZWFkIHYzKSBjb2RlXCIgPSBcIlRFUk1JRFwiKVxuICApICU+JVxuICByZW5hbWUoVGVybSA9IFRFUk0zMClcbmBgYCJ9 -->

```r
PSP_GPlevel <- PSP_GPlevel %>%
  left_join(
    CTV_library %>% select(TERMID, TERM30),
    by = c("CTV3 (Read v3) code" = "TERMID")
  ) %>%
  rename(Term = TERM30)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Analysis - air pollution

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVjRzlzYkhWMGFXOXVYM1JoWW14bElEd3RJRzFoZEdOb1pXUmZZV3hzSUNVK0pWeHVJQ0J6Wld4bFkzUW9ZRkJoY25ScFkybHdZVzUwSUVsRVlDd2dYRzRnSUNBZ0lDQWdJQ0JnWTJGelpXQXNYRzRnSUNBZ0lDQWdJQ0J3YjJ4c2RYUnBiMjVmZG1GeUlEMGdZRk4xYlcxbFpDQk5SVlFnYldsdWRYUmxjeUJ3WlhJZ2QyVmxheUJtYjNJZ1lXeHNJR0ZqZEdsMmFYUjVJSHdnU1c1emRHRnVZMlVnTUdBcFhHNWNibkJ2Ykd4MWRHbHZibDkwWVdKc1pTQWxQaVZjYmlBZ1ozSnZkWEJmWW5rb1kyRnpaU2tnSlQ0bFhHNGdJSE4xYlcxaGNtbHpaU2hjYmlBZ0lDQnVJRDBnYmlncExGeHVJQ0FnSUcxbFpHbGhibDl3YjJ4c2RYUnBiMjRnUFNCdFpXUnBZVzRvY0c5c2JIVjBhVzl1WDNaaGNpd2dibUV1Y20wZ1BTQlVVbFZGS1N4Y2JpQWdJQ0JKVVZKZmNHOXNiSFYwYVc5dUlEMGdTVkZTS0hCdmJHeDFkR2x2Ymw5MllYSXNJRzVoTG5KdElEMGdWRkpWUlNrc1hHNGdJQ0FnYldWaGJsOXdiMnhzZFhScGIyNGdQU0J0WldGdUtIQnZiR3gxZEdsdmJsOTJZWElzSUc1aExuSnRJRDBnVkZKVlJTa3NJQ0FqSUdwMWMzUWdabTl5SUdOdmJuUmxlSFJjYmlBZ0lDQnpaRjl3YjJ4c2RYUnBiMjRnUFNCelpDaHdiMnhzZFhScGIyNWZkbUZ5TENCdVlTNXliU0E5SUZSU1ZVVXBYRzRnSUNsY2JtQmdZQ0o5IC0tPlxuXG5gYGByXG5wb2xsdXRpb25fdGFibGUgPC0gbWF0Y2hlZF9hbGwgJT4lXG4gIHNlbGVjdChgUGFydGljaXBhbnQgSURgLCBcbiAgICAgICAgIGBjYXNlYCxcbiAgICAgICAgIHBvbGx1dGlvbl92YXIgPSBgU3VtbWVkIE1FVCBtaW51dGVzIHBlciB3ZWVrIGZvciBhbGwgYWN0aXZpdHkgfCBJbnN0YW5jZSAwYClcblxucG9sbHV0aW9uX3RhYmxlICU+JVxuICBncm91cF9ieShjYXNlKSAlPiVcbiAgc3VtbWFyaXNlKFxuICAgIG4gPSBuKCksXG4gICAgbWVkaWFuX3BvbGx1dGlvbiA9IG1lZGlhbihwb2xsdXRpb25fdmFyLCBuYS5ybSA9IFRSVUUpLFxuICAgIElRUl9wb2xsdXRpb24gPSBJUVIocG9sbHV0aW9uX3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBtZWFuX3BvbGx1dGlvbiA9IG1lYW4ocG9sbHV0aW9uX3ZhciwgbmEucm0gPSBUUlVFKSwgICMganVzdCBmb3IgY29udGV4dFxuICAgIHNkX3BvbGx1dGlvbiA9IHNkKHBvbGx1dGlvbl92YXIsIG5hLnJtID0gVFJVRSlcbiAgKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucG9sbHV0aW9uX3RhYmxlIDwtIG1hdGNoZWRfYWxsICU+JVxuICBzZWxlY3QoYFBhcnRpY2lwYW50IElEYCwgXG4gICAgICAgICBgY2FzZWAsXG4gICAgICAgICBwb2xsdXRpb25fdmFyID0gYFN1bW1lZCBNRVQgbWludXRlcyBwZXIgd2VlayBmb3IgYWxsIGFjdGl2aXR5IHwgSW5zdGFuY2UgMGApXG5cbnBvbGx1dGlvbl90YWJsZSAlPiVcbiAgZ3JvdXBfYnkoY2FzZSkgJT4lXG4gIHN1bW1hcmlzZShcbiAgICBuID0gbigpLFxuICAgIG1lZGlhbl9wb2xsdXRpb24gPSBtZWRpYW4ocG9sbHV0aW9uX3ZhciwgbmEucm0gPSBUUlVFKSxcbiAgICBJUVJfcG9sbHV0aW9uID0gSVFSKHBvbGx1dGlvbl92YXIsIG5hLnJtID0gVFJVRSksXG4gICAgbWVhbl9wb2xsdXRpb24gPSBtZWFuKHBvbGx1dGlvbl92YXIsIG5hLnJtID0gVFJVRSksICAjIGp1c3QgZm9yIGNvbnRleHRcbiAgICBzZF9wb2xsdXRpb24gPSBzZChwb2xsdXRpb25fdmFyLCBuYS5ybSA9IFRSVUUpXG4gIClcbmBgYCJ9 -->

```r
pollution_table <- matched_all %>%
  select(`Participant ID`, 
         `case`,
         pollution_var = `Summed MET minutes per week for all activity | Instance 0`)

pollution_table %>%
  group_by(case) %>%
  summarise(
    n = n(),
    median_pollution = median(pollution_var, na.rm = TRUE),
    IQR_pollution = IQR(pollution_var, na.rm = TRUE),
    mean_pollution = mean(pollution_var, na.rm = TRUE),  # just for context
    sd_pollution = sd(pollution_var, na.rm = TRUE)
  )
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1mcmFtZS1iZWdpbiBleUp0WlhSaFpHRjBZU0k2ZXlKamJHRnpjMlZ6SWpwYkluUmliRjlrWmlJc0luUmliQ0lzSW1SaGRHRXVabkpoYldVaVhTd2libkp2ZHlJNk1pd2libU52YkNJNk5pd2ljM1Z0YldGeWVTSTZleUpCSUhScFltSnNaU0k2V3lJeUlNT1hJRFlpWFgxOUxDSnlaR1lpT2lKSU5ITkpRVUZCUVVGQlFVRkNaM1I1YVZSRWJXbDFRbWxaUjBKbldtMUNhRnBYVW1kYVoxVjVSMVpvUkZFNWVEQk1VbWRaVjBwcFFVaEZXVWRHWjFwUFJVWXdRbFpEVVUxYVRFRkNUVk00VVdkNVVWcDNRWEpuWmswMFRsRlFiMGhGVUU5Q0swRTFlbVpqUVV0SVIxbzNVVXBXUTNoYVpVeE9TVVJHVmpObGFHbHBPV3BFS3psSlpXUnliWE5QVkZwR2VDOUNNMjFqU1dOaVJVUk9iRWd2WldneVZ5OUdNblp0Y2xaaVJuTXhhSEpJYlVwMVlXNUdVVWxaUVRKSVJWRlJXbUpyZUU5S1ZXMU5kbnB2UVhsQ00wNVRWWHBOVXpnclNVdzRia3A2VTJ0emVEaHRSR2wyV2pKQlVXaHBRbVppYVc5WGNGUjZSa3RWYUdseFFUZG9URTF2ZGpFMFRUVkNhSGRwU1Vjdkt5OHZMeTlJTjNGTWF6Tk5VMmt5UlhWb1oyeDVjRk5UVjBwUGNXeEdVVWd4UVROdWIxZDBhbnBETUVFeVFXcFZlSGRsU1VGWFZFNXFSVnB2UVdZeWEyVjVRMVZ3ZFhOclduQllibHAxYlZwdk1ITjNSbVZsYTJkUE5raFNlSGRDTVUxRFRUQlhiVVp6VG05bmNtMVFObXBvVXpWaVlXdzFObHBvTkhObVJteDZSWEJPVTJNeVFXMXdObE5YZDFWSlVVZENOMmMwVGtGeVMwMXlUVXMwU0RWRmVXaGhja1psVTFnMVNVa3dPRXRXYmtvNFJFVjNTRGR1VDBWbVFVTkVabloyYlZsQlowRkJJbjA9IC0tPlxuXG48ZGl2IGRhdGEtcGFnZWR0YWJsZT1cImZhbHNlXCI+XG4gIDxzY3JpcHQgZGF0YS1wYWdlZHRhYmxlLXNvdXJjZSB0eXBlPVwiYXBwbGljYXRpb24vanNvblwiPlxue1wiY29sdW1uc1wiOlt7XCJsYWJlbFwiOltcImNhc2VcIl0sXCJuYW1lXCI6WzFdLFwidHlwZVwiOltcImludFwiXSxcImFsaWduXCI6W1wicmlnaHRcIl19LHtcImxhYmVsXCI6W1wiblwiXSxcIm5hbWVcIjpbMl0sXCJ0eXBlXCI6W1wiaW50XCJdLFwiYWxpZ25cIjpbXCJyaWdodFwiXX0se1wibGFiZWxcIjpbXCJtZWRpYW5fcG9sbHV0aW9uXCJdLFwibmFtZVwiOlszXSxcInR5cGVcIjpbXCJkYmxcIl0sXCJhbGlnblwiOltcInJpZ2h0XCJdfSx7XCJsYWJlbFwiOltcIklRUl9wb2xsdXRpb25cIl0sXCJuYW1lXCI6WzRdLFwidHlwZVwiOltcImRibFwiXSxcImFsaWduXCI6W1wicmlnaHRcIl19LHtcImxhYmVsXCI6W1wibWVhbl9wb2xsdXRpb25cIl0sXCJuYW1lXCI6WzVdLFwidHlwZVwiOltcImRibFwiXSxcImFsaWduXCI6W1wicmlnaHRcIl19LHtcImxhYmVsXCI6W1wic2RfcG9sbHV0aW9uXCJdLFwibmFtZVwiOls2XSxcInR5cGVcIjpbXCJkYmxcIl0sXCJhbGlnblwiOltcInJpZ2h0XCJdfV0sXCJkYXRhXCI6W3tcIjFcIjpcIjBcIixcIjJcIjpcIjI0ODBcIixcIjNcIjpcIjE4NzVcIixcIjRcIjpcIjI5NTQuMjVcIixcIjVcIjpcIjI4MTkuNjcxXCIsXCI2XCI6XCIyODI3LjM3NVwifSx7XCIxXCI6XCIxXCIsXCIyXCI6XCIyNDhcIixcIjNcIjpcIjE3NDZcIixcIjRcIjpcIjM1MjUuMDBcIixcIjVcIjpcIjI2NzUuNDc3XCIsXCI2XCI6XCIyNjg2Ljg0MlwifV0sXCJvcHRpb25zXCI6e1wiY29sdW1uc1wiOntcIm1pblwiOnt9LFwibWF4XCI6WzEwXSxcInRvdGFsXCI6WzZdfSxcInJvd3NcIjp7XCJtaW5cIjpbMTBdLFwibWF4XCI6WzEwXSxcInRvdGFsXCI6WzJdfSxcInBhZ2VzXCI6e319fVxuICA8XC9zY3JpcHQ+XG48XC9kaXY+XG5cbjwhLS0gcm5iLWZyYW1lLWVuZCAtLT5cbiJ9 -->


<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibnJvdyI6MiwibmNvbCI6Niwic3VtbWFyeSI6eyJBIHRpYmJsZSI6WyIyIMOXIDYiXX19LCJyZGYiOiJINHNJQUFBQUFBQUFCZ3R5aVREbWl1QmlZR0JnWm1CaFpXUmdaZ1V5R1ZoRFE5eDBMUmdZV0ppQUhFWUdGZ1pPRUYwQlZDUU1aTEFCTVM4UWd5UVp3QXJnZk00TlFQb0hFUE9CK0E1emZjQUtIR1o3UUpWQ3haZUxOSURGVjNlaGlpOWpEKzlJZWRybXNPVFpGeC9CM21jSWNiRURObEgvZWgyVy9GMnZtclZiRnMxaHJIbUp1YW5GUUlZQTJIRVFRWmJreE9KVW1NdnpvQXlCM05TVXpNUzgrSUw4bkp6U2tzeDhtRGl2WjJBUWhpQmZiaW9XcFR6RktVaGlxQTdoTE1vdjE0TTVCaHdpSUcvKy8vLy9IN3FMazNNU2kyRXVoZ2x5cFNTV0pPcWxGUUgxQTNub1d0anpDMEEyQWpVeHdlSUFXVE5qRVpvQWYya2V5Q1VwdXNrWnBYblp1bVpvMHN3RmVla2dPNkhSeHdCMU1DTTBXbUZzTm9ncm1QNmpoUzViYWw1NlpoNHNmRmx6RXBOU2MyQW1wNlNXd1VJUUdCN2c0TkFyS01yTUs0SDVFeWhhckZlU1g1SUkwOEtWbko4REV3SDduT0VmQUNEZnZ2bVlBZ0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["case"],"name":[1],"type":["int"],"align":["right"]},{"label":["n"],"name":[2],"type":["int"],"align":["right"]},{"label":["median_pollution"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["IQR_pollution"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["mean_pollution"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["sd_pollution"],"name":[6],"type":["dbl"],"align":["right"]}],"data":[{"1":"0","2":"2480","3":"1875","4":"2954.25","5":"2819.671","6":"2827.375"},{"1":"1","2":"248","3":"1746","4":"3525.00","5":"2675.477","6":"2686.842"}],"options":{"columns":{"min":{},"max":[10],"total":[6]},"rows":{"min":[10],"max":[10],"total":[2]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVYRzVjYm5kcGJHTnZlQzUwWlhOMEtIQnZiR3gxZEdsdmJsOTJZWElnZmlCallYTmxMQ0JrWVhSaElEMGdjRzlzYkhWMGFXOXVYM1JoWW14bEtWeHVZR0JnSW4wPSAtLT5cblxuYGBgclxuXG5cbndpbGNveC50ZXN0KHBvbGx1dGlvbl92YXIgfiBjYXNlLCBkYXRhID0gcG9sbHV0aW9uX3RhYmxlKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5cbndpbGNveC50ZXN0KHBvbGx1dGlvbl92YXIgfiBjYXNlLCBkYXRhID0gcG9sbHV0aW9uX3RhYmxlKVxuYGBgIn0= -->

```r


wilcox.test(pollution_var ~ case, data = pollution_table)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5cdFdpbGNveG9uIHJhbmsgc3VtIHRlc3Qgd2l0aCBjb250aW51aXR5IGNvcnJlY3Rpb25cblxuZGF0YTogIHBvbGx1dGlvbl92YXIgYnkgY2FzZVxuVyA9IDE2OTY1NSwgcC12YWx1ZSA9IDAuMjM0NFxuYWx0ZXJuYXRpdmUgaHlwb3RoZXNpczogdHJ1ZSBsb2NhdGlvbiBzaGlmdCBpcyBub3QgZXF1YWwgdG8gMFxuIn0= -->

```

	Wilcoxon rank sum test with continuity correction

data:  pollution_var by case
W = 169655, p-value = 0.2344
alternative hypothesis: true location shift is not equal to 0
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG48IS0tIHJuYi1zb3VyY2UtYmVnaW4gZXlKa1lYUmhJam9pWUdCZ2NseHVkQzUwWlhOMEtIQnZiR3gxZEdsdmJsOTJZWElnZmlCallYTmxMQ0JrWVhSaElEMGdjRzlzYkhWMGFXOXVYM1JoWW14bEtWeHVZR0JnSW4wPSAtLT5cblxuYGBgclxudC50ZXN0KHBvbGx1dGlvbl92YXIgfiBjYXNlLCBkYXRhID0gcG9sbHV0aW9uX3RhYmxlKVxuYGBgXG5cbjwhLS0gcm5iLXNvdXJjZS1lbmQgLS0+XG4ifQ== -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudC50ZXN0KHBvbGx1dGlvbl92YXIgfiBjYXNlLCBkYXRhID0gcG9sbHV0aW9uX3RhYmxlKVxuYGBgIn0= -->

```r
t.test(pollution_var ~ case, data = pollution_table)
```

<!-- rnb-source-end -->


<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5cdFdlbGNoIFR3byBTYW1wbGUgdC10ZXN0XG5cbmRhdGE6ICBwb2xsdXRpb25fdmFyIGJ5IGNhc2VcbnQgPSAwLjY3NTI2LCBkZiA9IDIxMi4zOCwgcC12YWx1ZSA9IDAuNTAwMlxuYWx0ZXJuYXRpdmUgaHlwb3RoZXNpczogdHJ1ZSBkaWZmZXJlbmNlIGluIG1lYW5zIGJldHdlZW4gZ3JvdXAgMCBhbmQgZ3JvdXAgMSBpcyBub3QgZXF1YWwgdG8gMFxuOTUgcGVyY2VudCBjb25maWRlbmNlIGludGVydmFsOlxuIC0yNzYuNzM0MyAgNTY1LjEyMjBcbnNhbXBsZSBlc3RpbWF0ZXM6XG5tZWFuIGluIGdyb3VwIDAgbWVhbiBpbiBncm91cCAxIFxuICAgICAgIDI4MTkuNjcxICAgICAgICAyNjc1LjQ3NyBcbiJ9 -->

```

	Welch Two Sample t-test

data:  pollution_var by case
t = 0.67526, df = 212.38, p-value = 0.5002
alternative hypothesis: true difference in means between group 0 and group 1 is not equal to 0
95 percent confidence interval:
 -276.7343  565.1220
sample estimates:
mean in group 0 mean in group 1 
       2819.671        2675.477 
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->

