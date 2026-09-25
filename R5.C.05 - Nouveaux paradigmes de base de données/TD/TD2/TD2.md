## Activities

1. Aggregation: Number of companies per country.

        inKey: numLine
        inValue: line (company)
        outKey: country
        outValue: 1

        Mapper(inKey, inValue)
        if (numLine != firstLine)
            outKey = getCountry(inValue)
            outValue = 1
            emitIntermediate(outKey, outValue)


        inKey: country
        inValue: list of 1
        outKey: country
        outValue: number of companies in the country

        Reduce(inKey, inValue)
            outKey = inKey
            sum = 0
            foreach element of inValue
                sum++
            outValue = sum
            emit(outKey, outValue)

2. Aggregation: Number of platform per company.

        inKey: numLine
        inValue: line (platform)
        outKey: company
        outValue: 1

        Mapper(inKey, inValue)
        if (numLine != firstLine)
            outKey = getCompany(inValue)
            outValue = 1
            emitIntermediate(outKey, outValue)

        inKey: company
        inValue: list of 1
        outKey: company
        outValue: number of platform in the company

        Reduce(inKey, inValue)
            outKey = inKey
            sum = 0
            foreach element of inValue
                sum++
            outValue = sum
            emit(outKey, outValue)


3. Project: Name of the companies.

        inKey: numLine
        inValue: line (company)
        outKey: companyName
        outValue: null

        Mapper(inKey, inValue)
        if (numLine != firstLine)
            outKey = getCompanyName(inValue)
            outValue = null
            emitIntermediate(outKey, outValue)

        inKey: companyName
        inValue: list of null
        outKey: companyName
        outValue: null

        Reduce(inKey, inValue)
            outKey = inKey
            outValue = null
            emit(outKey, outValue)        

4. Project: Name of the platforms.

        inKey: numLine
        inValue: line (platform)
        outKey: platformName
        outValue: null

        Mapper(inKey, inValue)
        if (numLine != firstLine)
            outKey = getPlatformName(inValue)
            outValue = null
            emitIntermediate(outKey, outValue)

        inKey: platformName
        inValue: list of null
        outKey: platformName
        outValue: null

        Reduce(inKey, inValue)
            outKey = inKey
            outValue = null
            emit(outKey, outValue)

5. Selection: Platform with a price greater than 300$.

        inKey: numLine
        inValue: line (platform)
        outKey: line (platform)
        outValue: null

        Mapper(inKey, inValue)
        if (numLine != firstLine)
            if (getPrice(inValue) > 300)
            outKey = inValue
            outValue = null
            emitIntermediate(outKey, outValue)

        inKey: line (platform)
        inValue: list of null
        outKey: line (platform)
        outValue: null

        Reduce(inKey, inValue)
            outKey = inKey
            outValue = null
            emit(outKey, outValue)

6. Aggregation and comparison: Oldest companies per country.

        .

7. Comparison: Newest companies.

        .

8. Aggregation: Cheapest platform.

        .
