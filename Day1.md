# Intro - OOP Concepts and Dimension Tools, Basic Concepts - Scripting (MDD and its components)

# Info Items
    Metadata(en-US, Question, label)      
        Intro "Welcome to Kantar" info;
    End Metadata

    Routing(Web)
        Intro.Show()
    End Routing

# Text Questions
    Metadata(en-US, Question, label)      
        Q001 "What is your name" 
        text [1 .. 35];
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Single Response Categorical Question
    Metadata(en-US, Question, label)      
        Q001 "What is your gender?"
        categorical [1 .. 1]
        {
            _1 "Male",
            _2 "Female"
        };
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Multiple Response Categorical Question
    Metadata(en-US, Question, label)      
        Q001 "What car brands are you aware of?"
        categorical [1 .. ]
        {
            _1 "Toyota",
            _2 "Honda"
            _3 "Ferrari",
            _4 "BMW",
            _5 "Mercedes Benz"
        };
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Numeric Question - Long
    Metadata(en-US, Question, label)      
        Q001 "How old are you?"
        long [1 .. 99];
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Numeric Question - Double
    Metadata(en-US, Question, label)      
        Q001 "How much does your car worth?"
        double [1 .. 9999999];
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing
    
# Boolean Question
    Metadata(en-US, Question, label)      
        Q001 "This is a boolean question" boolean;
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Loop Question
    Metadata(en-US, Question, label)      
        Q001 "What different car brands are you aware of?"
        loop [1 .. 5] fields
        (
            slice "" text;
        ) expand;
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Grid Question
    Metadata(en-US, Question, label)      
        Q001 "Please rate the following cars." loop
        {
            _1 "Toyota",
            _2 "Honda"
            _3 "Ferrari",
            _4 "BMW",
            _5 "Mercedes Benz"
        } fields
        (
            slice "" 
            categorical [1 .. 1]
            {
                _1 "Very Poor",
                _2 "Poor",
                _3 "OK",
                _4 "Good",
                _5 "Very Good",
            }
        ) expand grid;

        Q002 "Can you tell me on how many of the following drinks you consumned each day last week?" loop
        {
            _1 "Tea",
            _2 "Coffee",
            _3 "Carbonated Soft Drinks",
            _4 "Milk",
            _5 "Fruit and Vegetables Drinks",
            _6 "Powdered Soft Drinks",
            _7 "Water"
        } fields
        (
            slice1 "Monday"
            long [0 .. 99]
            defaultanswer(0);

            slice2 "Tuesday"
            long [0 .. 99]
            defaultanswer(0);

            slice3 "Wednesday"
            long [0 .. 99]
            defaultanswer(0);

            slice4 "Thursday"
            long [0 .. 99]
            defaultanswer(0);

            slice5 "Friday"
            long [0 .. 99]
            defaultanswer(0);
        ) expand grid;
    End Metadata

    Routing(Web)
        Q001.Ask()

        Q002[..].slice1.MustAnswer = false
        Q002[..].slice2.MustAnswer = false
        Q002[..].slice3.MustAnswer = false
        Q002[..].slice4.MustAnswer = false
        Q002[..].slice5.MustAnswer = false
        Q002.Ask()
    End Routing

# Compound Question
    Metadata(en-US, Question, label)      
        Q001 "Compound Question Example" loop 
        {
            _1 "Brand 1",
            _2 "Brand 2",
            _3 "Brand 3"
        } fields 
        (
            slice1 ""
            categorical [1 .. ]
            {
                _1 "Option 1",
                _2 "Option 2"
            };

            slice2 ""
            categorical [1 .. 1]
            {
                _1 "Option 1",
                _2 "Option 2",
                _3 "Option 3"
            };

            slice3 "" long;
        ) expand;
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing

# Categorical using defined/shared list
    Metadata(en-US, Question, label)      
        List_Brands "" define
        {
            _1 "Brand 1",
            _2 "Brand 2",
            _3 "Brand 3",
            _4 "Brand 4",
            _5 "Brand 5"
        };

        Q001 "What brands are you aware of?" 
        categorical [1 .. ]
        {
            use List_Brands
        };
    End Metadata

    Routing(Web)
        Q001.Ask()
    End Routing