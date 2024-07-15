/*
 Chnageoil system 
 
 This script of ours is not finished yet but it works
 
 CREDITS
*/

#define OIL_WARNING_DISTANCE 20000 
#define OIL_BREAKDOWN_DISTANCE 25000 

new VehicleKilometers[MAX_VEHICLES]; 
new VehicleOilChanged[MAX_VEHICLES];

public OnPlayerEnterVehicle(playerid, vehicleid, ispassenger)
{
    if (VehicleKilometers[vehicleid] == 0)
    {
        VehicleKilometers[vehicleid] = 1;
        VehicleOilChanged[vehicleid] = 1; 
    }
    return 1;
}

public UpdateVehicleKilometers()
{
    for (new vehicleid = 1; vehicleid < MAX_VEHICLES; vehicleid++)
    {
        if (IsVehicleOccupied(vehicleid))
        {
            VehicleKilometers[vehicleid]++;
            
            if (VehicleKilometers[vehicleid] >= OIL_WARNING_DISTANCE && VehicleOilChanged[vehicleid] == 1)
            {
                new driverid = GetVehicleDriver(vehicleid);
                if (driverid != INVALID_PLAYER_ID)
                {
                    SendClientMessage(driverid, COLOR_YELLOW, "Warning: Your vehicle needs an oil change soon!");
                    VehicleOilChanged[vehicleid] = 0; 
                }
            }
            
            if (VehicleKilometers[vehicleid] >= OIL_BREAKDOWN_DISTANCE)
            {
                SetVehicleParamsEx(vehicleid, VEHICLE_PARAMS_UNSET, VEHICLE_PARAMS_UNSET, VEHICLE_PARAMS_UNSET, VEHICLE_PARAMS_UNSET, VEHICLE_PARAMS_UNSET, VEHICLE_PARAMS_UNSET, VEHICLE_PARAMS_UNSET);
                new driverid = GetVehicleDriver(vehicleid);
                if (driverid != INVALID_PLAYER_ID)
                {
                    SendClientMessage(driverid, COLOR_RED, "Your vehicle has broken down due to lack of oil change!");
                }
            }
        }
    }
    return 1;
}

CMD:changeoil(playerid, params[])
{
    new vehicleid = GetPlayerVehicleID(playerid);
    if (vehicleid != INVALID_VEHICLE_ID)
    {
        VehicleOilChanged[vehicleid] = 1;
        VehicleKilometers[vehicleid] = 0; // Reset kilometers after oil change
        SendClientMessage(playerid, COLOR_GREEN, "Oil change successful. Vehicle kilometers reset.");
    }
    else
    {
        SendClientMessage(playerid, COLOR_RED, "You must be in a vehicle to change the oil.");
    }
    return 1;
}
