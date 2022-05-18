# Day 2 - Question Types

# Important Notes
    Line Break - "<br/>"
    Showing Double Quotes on the Question Text - ""TEXT""
    OrderTypes:
        - ASC
        - DESC
        - RAN
        - REV
        - ROT
    OrderTypes on Routing:
        - oAscending
        - oCustom
        - oDescending
        - oNormal
        - oRandomize
        - oReverse
        - oRotate
    Canfilter - will always show
    Codes - makes the question non-mandatory
    [..1] - non-mandatory
    scale(value) - number of decimal places

# Info Items
    Metadata(en-US, Question, label)      
        INTRO_01 "Welcome! 
        Thank you for taking part of this survey. 
        Click '>' to begin." info;
    End Metadata

    Routing(Web)
        INTRO_01.Show()
    End Routing

# Categorical Questions - Single / Multi Response
    Metadata(en-US, Question, label)      
        GEN "Are you...?"
        categorical [1 .. 1]
        {
            _1 "Male",
            _2 "Female",
            _3 "Prefer not to answer"
        };

        OCCUP "Do you work in any of the following"
        categorical [1 .. ]
        {
            _1 "Advertising / Public Relations",
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _999 "None of these"
        };

    End Metadata

    Routing(Web)
        GEN.Ask()

        OCCUP.Ask()
    End Routing

# Shared List
    Metadata(en-US, Question, label)      
        Category_List "" define
        {
            _1 "Chips (corn based, flour base, etc.)",
            _2 "Baked Goods (brownies, packaged cakes, etc.)",
            _3 "Cookies (manufactured cookies)",
            _4 "Crackers",
            _5 "Wafer Products",
            _6 "Cereal",
            _7 "Donuts"
        };

        Q1 "How familiar are you with these types of snacks?"
        categorical [1 .. ]
        {
            use Category_List
        };

        Q2 "How most often you purchased below snacks?"
        categorical [1 .. ]
        {
            use Category_List
        };
    End Metadata

    Routing(Web)
        Q1.Ask()

        Q2.Categories = Q2.Categories = {_4}
        Q2.Ask()
    End Routing

# Category/Response List Order
    Metadata(en-US, Question, label)      
        Q1 "How familiar are you with these types of snacks?"
        categorical [1 .. ]
        {
            _1 "Chips (corn based, flour base, etc.)",
            _2 "Baked Goods (brownies, packaged cakes, etc.)",
            _3 "Cookies (manufactured cookies)",
            _4 "Crackers",
            _5 "Wafer Products",
            _6 "Cereal",
            _7 "Donuts"
        } ASC;

        Q2 "How often you purchased below snacks?"
        categorical [1 .. ]
        {
            _1 "Chips (corn based, flour base, etc.)",
            _2 "Baked Goods (brownies, packaged cakes, etc.)",
            _3 "Cookies (manufactured cookies)",
            _4 "Crackers",
            _5 "Wafer Products",
            _6 "Cereal",
            _7 "Donuts"
        };

        Q3 "How often you purchased below snacks?"
        categorical [1 .. ]
        {
            _1 "Chips (corn based, flour base, etc.)",
            _2 "Baked Goods (brownies, packaged cakes, etc.)",
            _3 "Cookies (manufactured cookies)",
            _4 "Crackers",
            _5 "Wafer Products",
            _6 "Cereal",
            _7 "Donuts"
        };
    End Metadata

    Routing(Web)
        Q1.Ask()

        Q2.Response.Order = OrderConstants.oAscending
        Q2.Ask()

        Q2.Categories.Order = {_3, _1, _2, _4, _6, _5, _7}
        Q3.Ask()
    End Routing

# Fix
    Metadata(en-US, Question, label)      
        Q1 "How familiar are you with these types of snacks?"
        categorical [1 .. ]
        {
            use Category_List,
            _999 "None of these" fix
        } ASC;
    End Metadata

    Routing(Web)
        Q1.Ask()
    End Routing

# Special Response Types
    Metadata(en-US, Question, label)      
        OCCUP "Do you work in any of the following?"
        categorical [1 .. ]
        {
            _1 "Advertising / Public Relations",
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _997 "None of these" NA,
            _998 "Refuse" REF,
            _999 "Don't know" DK
        };
    End Metadata

    Routing(Web)
        OCCUP.Ask()
    End Routing

# Exclusive
    Metadata(en-US, Question, label)      
        OCCUP "Do you work in any of the following?"
        categorical [1 .. ]
        {
            _1@ "Advertising / Public Relations" fix exclusive,
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _997 "None of these" NA,
            _998 "Refuse" REF,
            _999 "Don't know" DK
        };
    End Metadata

    Routing(Web)
        OCCUP.Ask()
    End Routing

# Other
    Metadata(en-US, Question, label)      
        PressRead "Do you work in any of the following?"
        categorical [1 .. ]
        {
            SundayTelegraph "Sunday Telegraph",
            SundayTimes "Sunday Times",
            Prima "Prima",
            Red "Red",
            ReadersDigest "Reader's Digest",
            LivingEtc "Living etc",
            OtherPleaseTypeIn "Other (Please type in)" other
        };
    End Metadata

    Routing(Web)
        OCCUP.Ask()
    End Routing

# Filtering Categories
    Metadata(en-US, Question, label)      
        OCCUP "Do you work in any of the following?"
        categorical [1 .. ]
        {
            _1 "Advertising / Public Relations",
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _999 "None of these" NA
        };

        OCCUP1 "Do you work in any of the following?"
        categorical [1 .. ]
        {
            _1 "Advertising / Public Relations",
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _999 "None of these" NA
        };
    End Metadata

    Routing(Web)
        OCCUP.Ask()

        OCCUP1.Categories.Filter = OCCUP.Response
        OCCUP1.Ask()
    End Routing

# Canfilter
    Metadata(en-US, Question, label)      
        OCCUP "Do you work in any of the following?"
        categorical [1 .. ]
        {
            _1 "Advertising / Public Relations",
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _999 "None of these" NA
        };

        OCCUP1 "Do you work in any of the following?"
        categorical [1 .. ]
        {
            _1 "Advertising / Public Relations",
            _2 "Marketing / Market Research",
            _3 "Manufacturer of snack products",
            _4 "Distributors/Sales/Promotion of snack products",
            _5 "Clothes Retailer",
            _999 "None of these" NA canfilter
        };
    End Metadata

    Routing(Web)
        OCCUP.Ask()

        OCCUP1.Categories.Filter = OCCUP.Response
        OCCUP1.Response
    End Routing

# Text Questions
    Metadata(en-US, Question, label)
        Chips "Can you think any more brands of <b>chips</b>?" text;

        Email "Please enter your email address here" text
        codes ({
            _999 "No Answer" NA,
        });

        ZipCode "What is your 5 digit zipcode?" 
        text [5 .. 5];
    End Metadata

    Routing(Web)
        Chips.Style.Control = ControlTypes.ctSingleLineEdit
        Chips.Ask()

        Email.MustAnswer = false
        Email.Ask()

        ZipCode.Ask()
    End Routing

# Controlling Min and Max Value on Routing
    Metadata(en-US, Question, label)
        ZipCode "What is your 5 digit zipcode?" 
        text;
    End Metadata

    Routing(Web)
        ZipCode.Validation.MinValue = 5
        ZipCode.Validation.MaxValue = 5
        ZipCode.Ask()
    End Routing

# Numeric Questions - Long and Double
    Metadata(en-US, Question, label)      
        AGE "Please type in your age" 
        long [0 .. 99];

        AGE_1 "Please type in your age" 
        long [0 .. 99]
        codes
        ({
            _999 "No Answer" NA
        });

        WEIGHT "What is your weight in kilograms?"
        double [47.5 .. 60] scale(2);
    End Metadata

    Routing(Web)
        AGE.Ask()

        AGE_1.MustAnswer = false
        AGE_1.Ask()

        WEIGHT.Ask()
    End Routing

# Stepped Values
    Metadata(en-US, Question, label)      
        CensusOnline "Which year's census returns would you most like to have available online?"
        long [1841..1901 step 10];
    End Metadata

    Routing(Web)
        CensusOnline.Ask()
    End Routing

# Loops
    Metadata(en-US, Question, label)      
        LoopV1 "Please answer the following question for each in your household"
        loop [1 .. 6] 
        fields
        (
            Name1 "Name"
            text [1 .. 100];

            Gender ""
            categorical [1 .. 1]
            {
                _1 "Male",
                _2 "Female"
            };

            ZipCode "Please enter your 5 digit ZipCode" text [5..5];
        ) expand;
    End Metadata

    Routing(Web)
        LoopV1[ .. ].Name1.Style.Control = ctControlTypes.ctSingleLineEdit
        LoopV1.Ask()
    End Routing

# Grids
    Metadata(en-US, Question, label)      
        Brands "Which of these brands do you think? Select all that apply."
        loop 
        {
            _1 "Has the exact taste I am looking for",
            _2 "Tasty",
            _3 "It has an appetizing aroma",
            _4 "Has a unique flavor",
            _5 "Low in fat",
        } fields
        (
            slice ""
            categorical [1 .. ]
            {
                _1 "Chips (corn based, flour base, etc.)",
                _2 "Baked Goods (brownies, packaged cakes, etc.)",
                _3 "Cookies (manufactured cookies)",
                _4 "Crackers",
                _5 "Wafer Products",
                _6 "Cereal",
                _7 "Donuts"
            };
        ) expand grid;
    End Metadata

    Routing(Web)
        Brands.Ask()
    End Routing

# Routing Logic
    Metadata(en-US, Question, label)      
        Q1 "Please select the brands that you like"
        categorical [1 .. ]
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson",
        };

        Q2 "Please select the most often used Brands"
        categorical [1 .. ]
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson",
        };

        Q3 "Please type in your age" long;

        ThankYou "Thank you for taking the survey" info;
    End Metadata

    Routing(Web)
        Q1.Ask()

        If ContainsAny(Q1, {_1}) then
            Q2.Ask()
        End if

        If Q3.Response > 18 then
            Q1.Ask()
            Q2.Ask()
        End if

        ThankYou.Show()
    End Routing

# Routing Logic with Filtering
    Metadata(en-US, Question, label)      
        Q1 "Please select the brands that you like"
        categorical [1 .. ]
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson",
        };

        Q2 "Please select the most often used Brands"
        categorical [1 .. ]
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson",
            _5 "Other"
        };
    End Metadata

    Routing(Web)
        Q1.Ask()

        If ContainsAny(Q1, {_1, _2}) then
            Q2.Categories = {} + Q1.Response + {_5}
            Q2.Ask()
        End if
    End Routing

# Logical Operators
    Metadata(en-US, Question, label)
        Q3 "Please type in your age" long;

        Q1 "Please select the brands that you like"
        categorical [1 .. ]
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson",
        };

        Q2 "Please select the most often used Brands"
        categorical [1 .. ]
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson",
        };

        ThankYou "Thank you for taking the survey" info;
    End Metadata

    Routing(Web)
        Q3.Ask()
        Q1.Ask()

        If Q3.Response > 18 AND ContainsAny(Q1, {_3}) then
            Q2.Categories = {} + Q1.Response + {_5}
            Q2.Ask()
        End if

        If NOT ContainsAny(Q2, {_3}) AND answercount(Q2) > 0 then
            ThankYou.Show()
        End if

    End Routing

# Select Case
    Metadata(en-US, Question, label)    
        Q1_Recoding "Age recoding"
        categorical [1 .. ]
        {
            _1 "Less than 18",
            _2 "18-34",
            _3 "35-54,
            _4 "55+"
        };

        Q2 "Please type in your age" long;
    End Metadata

    Routing(Web)
        Q2.Ask()

        Select Case Q2.Response.Value
            Case 1 to 17
                Q1_Recoding = {_1}
            Case 18 to 34
                Q1_Recoding = {_2}
            Case 35 to 54
                Q1_Recoding = {_3}
            Case > 54
                Q1_Recoding = {_4}
        End Select

        If IOM.info.IsDebug then Q1_Recoding.Show()
    End Routing

# Asking a specific category
    Metadata(en-US, Question, label)    
        LoopQ1 "" loop 
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson"
        } fields 
        (
            Q1 "Will you consider the brand {@} in future?"
            categorical [1 .. 1]
            {
                _1 "Yes",
                _2 "No"
            };

            Q2 "Why do you like this brand" text;
        ) expand;
    End Metadata

    Routing(Web)
        // Accessing the Nestle Brand 
        LoopQ1[{_1}].Ask()

        // Accessing only the Q1
        LoopQ1[{_1}].Q1.Ask()

        // Asking for all categories
        LoopQ1[..].Ask()

        // Asking only Q1 for all categories
        LoopQ1[..].Q1.Ask()
    End Routing

# For Each Loop
    Metadata(en-US, Question, label)    
        LoopQ1 "" loop 
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson"
        } fields 
        (
            Q1 "Will you consider the brand {@} in future?"
            categorical [1 .. 1]
            {
                _1 "Yes",
                _2 "No"
            };

            Q2 "Why do you like this brand" text;
        ) expand;
    End Metadata

    Routing(Web)
        Dim Cat_Q1
        For each Cat_Q1 in LoopQ1.Categories
            LoopQ1[Cat_Q1].Q1.Ask()
            If ContainsAny(LoopQ1[Cat_Q1].Q2, {_1})
                LoopQ1[Cat_Q1].Q2.Ask()
            End if
        Next
    End Routing

# For Loop
    Metadata(en-US, Question, label)    
        LoopQ1 "" loop 
        {
            _1 "Nestle",
            _2 "P&G",
            _3 "Unilever",
            _4 "Johnson & Johnson"
        } fields 
        (
            Q1 "Will you consider the brand {@} in future?"
            categorical [1 .. 1]
            {
                _1 "Yes",
                _2 "No"
            };

            Q2 "Why do you like this brand" text;
        ) expand;
    End Metadata

    Routing(Web)
        Dim i
        For i = 0 to LoopQ1.Categories.Count - 1
            LoopQ1[i].Q1.Ask()
        Next
    End Routing