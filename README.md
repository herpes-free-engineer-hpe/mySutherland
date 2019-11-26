Transport package using Sutherland's formula for dynamic viscosity,
while considering a constant Prandtl number for thermal conductivity instead
of the Eucken formula used in OpenFOAM's implementation.

Compile with `wmake libso` and refer to `libmyspecie.so` in the controlDict.

Usage example
-------------

    /*--------------------------------*- C++ -*----------------------------------*\
      =========                 |
      \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
       \\    /   O peration     | Website:  https://openfoam.org
        \\  /    A nd           | Version:  7
         \\/     M anipulation  |
    \*---------------------------------------------------------------------------*/
    FoamFile
    {
        version     2.0;
        format      ascii;
        class       dictionary;
        location    "constant";
        object      thermophysicalProperties;
    }
    // * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

    thermoType
    {
        type            hePsiThermo;
        mixture         pureMixture;
        transport       mySutherland;
        thermo          hConst;
        equationOfState perfectGas;
        specie          specie;
        energy          sensibleInternalEnergy;
    }

    mixture // air at room temperature (300 K)
    {
        specie
        {
            molWeight   28.96;
        }
        thermodynamics
        {
            Cp          1006.3;
            Hf          0;
        }
        transport
        {
            As          1.458e-06;
            Ts          110.4;
            Pr          0.72;
        }
    }

    // ************************************************************************* //
