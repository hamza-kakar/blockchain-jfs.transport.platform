
### Register Broker

```
{
  "$class": "jfs.transport.platform.Broker",
  "businessName": "br1",
  "dotNumber": "br1",
  "address": "br1",
  "licenseDetails": "br1",
  "proofOfInsurance": "br1",
  "numberOfTripsConducted": 0,
  "numberOfTripsCompleted": 0,
  "numberOfDamageFreeShipping": 0,
  "claimsHistoy": "br1",
  "uId": "br1",
  "email": "br1",
  "password": "br1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.Broker 

```

### Register Carrier

```
{
  "$class": "jfs.transport.platform.Carrier",
  "businessName": "ca1",
  "dotNumber": "ca1",
  "address": "ca1",
  "operatingName": "ca1",
  "website": "ca1",
  "registrationDate": "2018-10-22T06:47:06.755Z",
  "licenseDetails": "ca1",
  "numberOfTripsConducted": 0,
  "numberOfTripsCompleted": 0,
  "numberOfDamageFreeShipping": 0,
  "claimsHistoy": "ca1",
  "uId": "ca1",
  "email": "ca1",
  "password": "ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.Carrier 

```

### Register Driver

this will be done by a carrier. in example given below the Carrier with id "ca1" is registering his Driver of id "dr1"</br>

```
{
  "$class": "jfs.transport.platform.Driver",
  "companyId": "dr1",
  "firstName": "dr1",
  "middleName": "dr1",
  "lastName": "dr1",
  "dob": "2018-10-22T06:54:56.902Z",
  "licenseNumber": "dr1",
  "licenseExpiry": "2018-10-22T06:54:56.902Z",
  "licenseIssuedAuthority": "dr1",
  "licenseIssuedProvince": "dr1",
  "milesDriven": 0,
  "numberOfClaimsIncidents": 0,
  "numberOfTripsCompleted": 0,
  "damageFreeTrips": 0,
  "certificationsTrainings": "dr1",
  "eldHosRecords": "dr1",
  "drivingHistory": "dr1",
  "uId": "dr1",
  "email": "dr1",
  "password": "dr1",
  "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.Driver

```

### Register Truck

this will be done by a carrier. in example given below the Carrier with id "ca1" is registering his Truck of id "tr1"</br>

```
{
  "$class": "jfs.transport.platform.Truck",
  "vin": "tr1",
  "numberPlate": "tr1",
  "make": "tr1",
  "model": "tr1",
  "odometerReading": "tr1",
  "ownerInfo": "tr1",
  "purchaseDate": "2018-10-22T07:00:13.736Z",
  "numberOfClaimsIncidents": 0,
  "uId": "tr1",
  "email": "tr1",
  "password": "tr1",
  "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.Truck
 
```



### (1) Register Load

this will be done by a broker. in example given below the Broker with id "b1" is registering a load of id "l1"</br>
"typeOfLoad" are predefined types. for right now the types are:
* TYPE1
* TYPE2
* TYPE3

```
{
  "$class": "jfs.transport.platform.Load",
  "loadId": "lo1",
  "proofOfDelivery": "l1",
  "typeOfLoad": "TYPE1",
  "pickUpLocation": "lo1",
  "deliveryLocation": "lo1",
  "consigneeDetails": "lo1",
  "FreightBill": "lo1",
  "status": "INITIATED",
  "broker": "resource:jfs.transport.platform.Broker#br1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.Load

 
```


### (2) Assign Carrier

this will be done by a broker. in example given below the Broker with id "br1" is assigning a load of id "lo1" to a Carrier of id "ca1"</br>
<b>Operations performed:</b>
* increments `numberOfTripsConducted` of carrier
* inserts new category in `typeOfLoadsHandled` if type is new.
* inserts carrier id to `carrier` in selected load. (assigns carrier to load)

```
{
 "$class": "jfs.transport.platform.AssignCarrier",
 "billOfLanding": "xyz",
 "load": "resource:jfs.transport.platform.Load#lo1",
 "broker": "resource:jfs.transport.platform.Broker#br1",
 "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.AssignCarrier
 
```


### (3) Assign Truck

this will be done by a Carrier. in example given below the Carrier with id "ca1" is assigning a load of id "lo1"  to Driver of id "dr1". A `pickUpTime` (load pickup time) is also required for this operation.</br>

<b>Operations performed:</b>
* inserts the `pickUpTime` to Load. 
* inserts truck id to `truck` in selected load. (assigns truck to load)
* updates the load `status` to "TRUCK_ASSIGNED". 

```
{
  "$class": "jfs.transport.platform.AssignTruck",
  "pickUpTime": "2018-10-23T05:21:49.475Z",
  "load": "resource:jfs.transport.platform.Load#lo1",
  "truck": "resource:jfs.transport.platform.Truck#tr1",
  "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.AssignTruck
 
```

### (4) Assign Driver

this will be done by a Carrier. in example given below the Carrier with id "ca1" is assigning a load of id "lo1"  to Driver of id "dr1".</br>
<b>Operations performed:</b>
* inserts driver id to `driver` in selected load. (assigns driver to load)
* updates the load `status` to "DRIVER_ASSIGNED". 

```
{
  "$class": "jfs.transport.platform.AssignDriver",
  "load": "resource:jfs.transport.platform.Load#lo1",
  "driver": "resource:jfs.transport.platform.Driver#dr1",
  "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.AssignDriver
 
```

### (5) Mark Dispached

this will be done by a Carrier. it actually means that the driver and truck with the load have left for their destination and are on way to delivery location.</br>
<b>Operations performed:</b>
* updates the load `status` to "DISPACHED". 

```
{
  "$class": "jfs.transport.platform.MarkDispached",
  "load": "resource:jfs.transport.platform.Load#lo1",
  "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.MarkDispached
 
```

### (6) Mark Delivered

this will be done by a Carrier. it actually means that the driver and truck with the load have delivered the load to delivery location. The `deliveryTime`, `milesDriven` and `consignorDetails` are also required for this operation.</br>
<b>Operations performed:</b>
* updates the load `status` to "DELIVERED".
* inserts `deliveryTime` in load.
* inserts `consignorDetails` in load.
* adds `milesDriven` during trip to `milesDriven` of Driver.

```
{
  "$class": "jfs.transport.platform.MarkDelivered",
  "milesDriven": 100,
  "deliveryTime": "2018-10-23T05:45:22.439Z",
  "consignorDetails": "xyz",
  "load": "resource:jfs.transport.platform.Load#lo1",
  "carrier": "resource:jfs.transport.platform.Carrier#ca1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.MarkDelivered
 
```

### (7..) Approve Delivered

this will be done by a Broker. the broker approves that load has been delivered to delivery location.
Broker can also insert a Claim and that claim contains a description and damageStatus (optional). </br>
<b>Operations performed:</b>
* updates the load `status` to "DELIVERED_APPROVED".
* inserts `claim` to driver and truck.(in case of claim)
* increments `numberOfClaimsIncidents` of truck and driver.(in case of claim)
* in crements `damageFreeTrips` of broker,carrier and driver. (in case of no claim or claim with no damage)
* inserts `typeOfTripCompleted` in driver.
* inserts `numberOfTripsCompleted` in broker,carrier and driver.

<b>approve without a claim:</b>
```
{
  "$class": "jfs.transport.platform.ApproveDelivered",
  "load": "resource:jfs.transport.platform.Load#lo1",
  "broker": "resource:jfs.transport.platform.Broker#br1"
}

```
<b>approve with a claim (with no damage to load):</b>
```
{
  "$class": "jfs.transport.platform.ApproveDelivered",
  "claim": {
    "$class": "jfs.transport.platform.Claim",
    "description": "xyz",
    "damageStatus": flase,
    "load": "resource:jfs.transport.platform.Load#lo1"
  },
  "load": "resource:jfs.transport.platform.Load#lo1",
  "broker": "resource:jfs.transport.platform.Broker#br1"
}

```

<b>approve with a claim (with damage to load):</b>
```
{
  "$class": "jfs.transport.platform.ApproveDelivered",
  "claim": {
    "$class": "jfs.transport.platform.Claim",
    "description": "xyz",
    "damageStatus": true,
    "load": "resource:jfs.transport.platform.Load#lo1"
  },
  "load": "resource:jfs.transport.platform.Load#lo1",
  "broker": "resource:jfs.transport.platform.Broker#br1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.ApproveDelivered
 
```

### (7..) Decline Delivered

this will be done by a Broker. in case the load is not delivered to location</br>
<b>Operations performed:</b>
* updates the load `status` to "DILEVERED_DECLINED".

```
{
  "$class": "jfs.transport.platform.DeclineDelivered",
  "load": "resource:jfs.transport.platform.Load#lo1",
  "broker": "resource:jfs.transport.platform.Broker#br1"
}

```
##### Request URL 
``` 
http://35.175.131.198:3000/api/jfs.transport.platform.DeclineDelivered
 
```
