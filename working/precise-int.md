___

## Static methods of the PreciseInt
___

### PreciseInt.IsNaN(PreciseInt number)
The `IsNaN` static method returns a boolean of whether `number` is NaN. To do so, it does the following steps:

1. let `result` equal to the `number`'s `isNaN` property.
2. return `result`

___

### PreciseInt.IsFinite(PreciseInt number)
The `IsFinite` static method returns a boolean of whether `number` is Infinity. To do so, it does the following steps:

1. let `result` equal to the `number`'s `isInfinity` property
2. if `result` equals `true`

    a. Return `false`

3. else

    a. Return `true`

___

## Static properties of the PreciseInt
___

### PreciseInt.bases
The `bases` property of `PreciseInt` should be a readonly list of string values of length 36, containing the following values (in order): `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `A`, `B`, `C`, `D`, `E`, `F`, `G`, `H`, `I`, `J`, `K`, `L`, `M`, `N`, `O`, `P`, `Q`, `R`, `S`, `T`, `U`, `V`, `W`, `X`, `Y`, `Z`

___

### PreciseInt.NaN
The `NaN` property of `PreciseInt` should be a readonly PreciseInt who's `isNaN` property is set to `true`

___

### PreciseInt.POSITIVE_INFINITY
The `POSITIVE_INFINITY` property of `PreciseInt` should be a readonly PreciseInt who's `isInfinity` property is set to `true`, and `IsNegative` property is set to `false`

___

### PreciseInt.NEGATIVE_INFINITY
The `NEGATIVE_INFINITY` property of `PreciseInt` should be a readonly PreciseInt who's `isInfinity` property is set to `true`, and `IsNegative` property is set to `true`

___

## Methods of the PreciseInt instance
___

### PreciseInt#Add(IPreciseNumber otherNumber)
The instance method `Add` adds `this` and `otherNumber` together, returning the result. To do so, it performs the following steps:

1. if `otherNumber` is __NaN__ or this precise int is __NaN__, return __NaN__
2. let `convertedNumber` equal to the result of calling `otherNumber.ConvertToBase(this.Base)`
3. Create a new list called `placesResult`
4. Loop through each place in `convertedNumber` and `this`, adding them together and pushing the result to `placesResult`. If the length of places in`this` and `convertedNumber` is not the same, `0`'s should be added to the front of the number with a lower length of digits until they are the same length.
5. let `result` equal a new PreciseInt, setting `Base` to `this.Base`, and `places` to `placesResult`
6. let `resultCleanedUp` equal to the result of calling `result.Cleanup()`
7. Return `resultCleanedUp`

___

### PreciseInt#Subtract(IPreciseNumber otherNumber)
The instance method `Subtract` subtracts `otherNumber` from `this`, returning the result. To do so, performs the following steps:

1. if `otherNumber` is __NaN__ or this precise int is __NaN__, return __NaN__
2. let `invertedOtherNumber` equal to the result of calling `otherNumber.Invert()`
3. return the result of calling `this.Add(invertedOtherNumber)`

___

### PreciseInt#Multiply(IPreciseNumber otherNumber)

___

### PreciseInt#Divide(IPreciseNumber otherNumber)

1. Let `dividing` equal to the first digit in this precise int.
2. Let `index` be an integer with the value of `1`
3. Todo

___

### PreciseInt#Invert()
The instance method `Invert` inverts the sign of `this`. To do so, it performs the following steps:

1. if this precise int is __NaN__, return __NaN__
2. let `newPlaces` equal a new list.
3. loop through all places in this precise int, adding each one to `newPlaces`.
4. let `result` equal to a new precise int, with the `places` property set to `newPlaces`, the `Base` property set to `this.Base`, the `IsNegative` property set to the opposite of `this.IsNegative`, and the `isInfinity` set to `this.isInfinity`
5. return `result`

___

### PreciseInt#ConvertToBase(Number newBase)
The instance method `ConvertToBase` converts this precise int to the given base and returns the new, converted number. To do so, it performs the following steps:

1. if `newBase` is less than 2, or if `newBase` is greater than `36`

    a. Throw a new RangeError/ArgumentOutOfRangeException
2. todo

___

### PreciseInt#RemoveLeadingZeros()
The instance method `RemoveLeadingZeros` converts this precise int to a new precise int without leadiing zeros. To do so, it performs the following steps:

1. if this precise int is __NaN__, return __NaN__
2. let `newPlaces` equal a new list
3. let `dontAddPlaces` equal to `true`
4. loop through each place in this precise int's places, where `index` is the current index in `places`, and `length` is the length of the `places` list, from index `0` to index `length - 1`, where `place` is the current place

    a. if `dontAddPlaces` equals `true`

        i. if `index` + 1 equals `length` or `place` does not equal `0`, set `dontAddPlaces` to `false`

    b. if `dontAddPlaces` equals `false`

        i. Add `place` to the `newPlaces` list

5. let `result` equal a new PreciseInt, with the `places` property set to `newPlaces`, the `Base` set to this precise int's `Base` property value, the `IsNegative` property set to this precise int's `IsNegative` property value, and the `isInfinity` property set to this precise int's `isInfinity` property value.
6. Return `result`

___

### PreciseInt#Cleanup()
The instance method `Cleanup` converts this precise int to a new precise int, cleaning up leading zeros, and overflow on the `places` property. To do so, it does the following steps:

1. let `fixedOverflowNumber` equal to the result of calling this precise int's `ConvertToBase` method, with the argument of `newBase` set to this precise int's base.
2. let `result` equal to calling `RemoveLeadingZeros` method on the `fixedOverflowNumber` variable
3. Return `result`

___

### PreciseInt#ToString()
The instance method `ToString` converts this precise int to a string. To do so, it does the following steps:

1. if this precise int's `isNaN` property is `true`, return a new string, who's string value is `NaN`
2. let `result` equal a new, empty string.
3. if this precise int's `IsNegative` property is `true`:

    a. set `result` to the string concatenation of `result` and the string value `-`

4. if this precise int's `isInfinity` property is `true`:

    a. set `result` to the string concatenation of `result` and the string value `Infinity`
    b. return `result`

5. loop through each place in this precise int's `places`, letting `index` be the current index, the `length` being the length of the precise int's places list, while `index` is less than `length`:

    a. let `place` equal to getting the value at index `index` in this precise int's `places` list.
    b. let `stringedPlace` equal to getting the value at index `place` in the precise int's static `bases` property.
    c. set `result` to the string concatenation of `result` and `stringedPlace`

6. return `result`

___

## Properties of the PreciseInt instance
___

### PreciseInt#places
The `places` property is a list of numbers containing all place values for this instance.

___

### PreciseInt#SupportsDecimals
The `SupportsDecimals` property is a boolean of whether or not this precise number supports decimals. Should be a `readonly` property who's value is `false`.

___

### PreciseInt#Base
The `Base` property is a number indicating what base this precise number is in. Defaults to base `10`.

___

### PreciseInt#IsNegative
The `IsNegative` property is a boolean indicating if this precise integer is negative

___

### PreciseInt#isNaN
The `isNaN` property is a boolean indicating if this precise integer is `NaN`. Should be set in the constructor of `PreciseInt`, and thus should be `readonly`

___

### PreciseInt.#isInfinity
The `isInfinity` property is a boolean indicating whether this number is `infinity`. Should be set in the constructor of `PreciseInt`, and thus should be `readonly`
