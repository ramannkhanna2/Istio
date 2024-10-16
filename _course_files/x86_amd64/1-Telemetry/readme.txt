--- Kiali Dynamic Traffic Routing


 -- go to Services >> Namespace: default >> fleetman-staff-service    and suspend traffic ...
  -- check the traffic has been suspended to staff service ,,,
     --- u ll ntce on application , now driver information wl not show up

  --- again resume the svc by remoing that suspension by clicking on Delte all traffic routig from Kiali...



--- Using Jaeger UI

  -- open jaeger ui , select webapp default service >> select custom time range >> starting from time now to next day ...
  --- browse the application to collect traces on jagger 
  --- check for traces and spans for http request travel among diff microservices .