# Big Data - MapReduce

## 4 Activities

1. Number of companies per city.

        var map = function() {
            if (this.city) {
                emit(this.city, 1);
            }
        };

        var reduce = function(key, values) {
            return Array.sum(values);
        };

        db.company.mapReduce(
            map, reduce, { out: "NbCity" }
        );

        db.NbCity.find();

2. Names of the companies.

        var map = function() {
            emit(this.name, null);
        };

        var reduce = function(key, values) {
            return Array.sum(values);
        };

        db.company.mapReduce(map, reduce, { out: "Companies" });
        db.Companies.find({}, { _id: 1 });

3. Companies where country is France.

        var map = function() {
            if (this.country === "France") {
                emit(this.name, null);
            }
        };

        var reduce = function(key, values) {
            return Array.sum(values);
        };

        db.company.mapReduce(map, reduce, { out: "FRCompagny" });
        db.FRCompagny.find({}, { _id: 1 });

4. Most expensive platform per company.

        var map = function() {
            if (this.company && this.price !== undefined) {
                emit(this.company, { 
                    platform: this.name, 
                    price: Number(this.price) 
                });
            }
        };

        var reduce = function(key, values) {
            var max = values[0];
            for (var i = 1; i < values.length; i++) {
                if (values[i].price > max.price) {
                    max = values[i];
                }
            }
            return max;
        };

        db.platform.mapReduce(map, reduce, { out: "ExpensivePlatform" });
        db.ExpensivePlatform.find();

5. Oldest company.

        var map = function() {
            if (this.creation && this.name) {
                emit(1, { 
                    name: this.name, 
                    creation: this.creation 
                });
            }
        };

        var reduce = function(key, values) {
            var max = values[0];
            for (var i = 1; i < values.length; i++) {
                if (values[i].creation < max.creation) {
                    max = values[i];
                }
            }
            return max;
        };

        db.company.mapReduce(map, reduce, { out: "OldestCompany" });
        db.OldestCompany.find();


6. Country with the maximum number of companies.

        var map = function() {
            if (this.country) {
                emit(this.country, 1);
            }
        };

        var reduce = function(key, values) {
            return Array.sum(values);
        };

        db.company.mapReduce(map, reduce, { out: "companiesPerCountry" });
        db.companiesPerCountry.find().sort({ value: -1 }).limit(1);
