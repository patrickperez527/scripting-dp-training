# Day 3

# Shared List
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

        Q002 "What brands are you not aware of?" 
        categorical [1 .. ]
        {
            use List_Brands
        };
    End Metadata

    Routing(Web)
        Q001.Ask()
        Q002.Ask()
    End Routing

# Page
    Metadata(en-US, Question, label)      
        S1 "What is your name?" text;

        S2 "How old are you?" long [1 .. 100];

        S3 "Are you a college graduate?"
        categorical [1 .. 1]
        {
            _1 "Yes",
            _2 "No"
        };

        PageS1_S2 "" page
        (
            S1, 
            S2,
            S3
        );
    End Metadata

    Routing(Web)
        PageS1_S2.Ask()
    End Routing

# Filtering Page
    Metadata(en-US, Question, label)      
        S1 "What is your name?" text;

        S2 "How old are you?" long [1 .. 100];

        S3 "Are you a college graduate?"
        categorical [1 .. 1]
        {
            _1 "Yes",
            _2 "No"
        };

        PageS1_S2 "" page
        (
            S1, 
            S2,
            S3
        );

        N2 "Which decade you born in, select the nearest decade? <br/> (e.g., if you born between 1980 to 1984 then use 1980, if you born in 1985 to 1989 then use 1990)"
        long [1950 .. 2020 step 10];
    End Metadata

    Routing(Web)
        N2.Ask()

        If N2.Response >= 1950 AND N2.Response <= 1990
            PageS1_S2.QuestionFilter = "S1, S3"
        Else
            PageS1_S2.QuestionFilter = "S2, S3"
        End If

        PageS1_S2.Ask()
    End Routing

# Block
    Metadata(en-US, Question, label)      
        Metadata(en-US, Question, label)      
        S1 "What is your name?" text;

        S2 "How old are you?" long [1 .. 100];

        S3 "Are you a college graduate?"
        categorical [1 .. 1]
        {
            _1 "Yes",
            _2 "No"
        };

        BlockS1_S2 "" block fields
        (
            S1 "What is your name?" text;

            S2 "How old are you?" long [1 .. 100];

            S3 "Are you a college graduate?"
            categorical [1 .. 1]
            {
                _1 "Yes",
                _2 "No"
            };
        );
    End Metadata

    Routing(Web)
        BlockS1_S2.Ask()
    End Routing

# Subheadings
    Metadata(en-US, Question, label)      
        OrganicFood "There is an increasing interest in organically produced food. What are your thoughts about this?" 
        categorical [1..]
        {
            AgainstOrganicFood "Thoughts against"
            {
                Expensive "It's too expensive",
                NotGoodLandUse "It doesn't make the best use of the land",
                NotProven "There's no proof it's better than other food",
                LaborIntensive "It's too labor intensive",
                OtherNegative "Other thoughts against" other
            },

            ForOrganicFood "Thoughts for"
            {
                GoodForYou "It's good for you",
                BuyItMyself "I buy organic food whenever I can",
                GoodForLand "It's better for land",
                GoodforWildlife "It's better for wildlife",
                OtherPositive "Other thoughts for" other
            },
            
            NoThoughts "I have no opinions about organic food" fix exclusive
        } ran;

    End Metadata

    Routing(Web)
        // Accessing AgainstOrganicFood
        OrganicFood.Categories[{AgainstOrganicFood}]

        // Accessing AgainstOrganicFood Category 1
        OrganicFood.Categories[{AgainstOrganicFood}].Categories[{_1}]

        OrganicFood.Ask()
    End Routing

# Subheadings (For Loop)
    Metadata(en-US, Question, label)      
        OrganicFood "There is an increasing interest in organically produced food. What are your thoughts about this?" 
        loop
        {
            AgainstOrganicFood "Thoughts against"
            {
                Expensive "It's too expensive",
                NotGoodLandUse "It doesn't make the best use of the land",
                NotProven "There's no proof it's better than other food",
                LaborIntensive "It's too labor intensive",
                OtherNegative "Other thoughts against" other
            },

            ForOrganicFood "Thoughts for"
            {
                GoodForYou "It's good for you",
                BuyItMyself "I buy organic food whenever I can",
                GoodForLand "It's better for land",
                GoodforWildlife "It's better for wildlife",
                OtherPositive "Other thoughts for" other
            },
            
            NoThoughts "I have no opinions about organic food" fix exclusive
        } ran fields
        (
            scale ""
            categorical [1 .. 1]
            {
                _1 "Yes",
                _2 "No"
            };
        );

    End Metadata

    Routing(Web)
        OrganicFood.Ask()

        Dim Cat_OrganicFood, Inner_Cat_OrganicFood, Count_OrganicFood
        For Each Cat_OrganicFood in OrganicFood.Categories
            For Each Inner_Cat_OrganicFood in Cat_OrganicFood.Categories
                If ContainsAny(OrganicFood[Inner_Cat_OrganicFood].scale, {_1}) Then
                    Count_OrganicFood = Count_OrganicFood + 1
                End If
            Next
        Next;

        Debug.MsgBox(Count_OrganicFood)
    End Routing

# Applying Order Types On Subheading
    Metadata(en-US, Question, label)      
        OrganicFood "There is an increasing interest in organically produced food. What are your thoughts about this?" 
        categorical [1..]
        {
            AgainstOrganicFood "Thoughts against"
            {
                Expensive "It's too expensive",
                NotGoodLandUse "It doesn't make the best use of the land",
                NotProven "There's no proof it's better than other food",
                LaborIntensive "It's too labor intensive",
                OtherNegative "Other thoughts against" other
            } ran,

            ForOrganicFood "Thoughts for"
            {
                GoodForYou "It's good for you",
                BuyItMyself "I buy organic food whenever I can",
                GoodForLand "It's better for land",
                GoodforWildlife "It's better for wildlife",
                OtherPositive "Other thoughts for" other
            } ran,
            
            NoThoughts "I have no opinions about organic food" fix exclusive
        } ran;

    End Metadata

    Routing(Web)
        OrganicFood.Ask()
    End Routing

# Text Insertion Through Routing
    Metadata(en-US, Question, label)      
        OrganicFood "There is an increasing interest in organically produced food. What are your thoughts about this? <br/>{ins}" 
        loop
        {
            AgainstOrganicFood "Thoughts against"
            {
                Expensive "It's too expensive",
                NotGoodLandUse "It doesn't make the best use of the land",
                NotProven "There's no proof it's better than other food",
                LaborIntensive "It's too labor intensive",
                OtherNegative "Other thoughts against" other
            },

            ForOrganicFood "Thoughts for"
            {
                GoodForYou "It's good for you",
                BuyItMyself "I buy organic food whenever I can",
                GoodForLand "It's better for land",
                GoodforWildlife "It's better for wildlife",
                OtherPositive "Other thoughts for" other
            },
            
            NoThoughts "I have no opinions about organic food" fix exclusive
        } ran fields
        (
            scale ""
            categorical [1 .. 1]
            {
                _1 "Yes",
                _2 "No"
            };
        );

    End Metadata

    Routing(Web)
        OrganicFood.Inserts["ins"] = "Please select answer for each row."
        OrganicFood.Ask()
    End Routing

# Text Insertion on Category Label
    Metadata(en-US, Question, label)      
        Q001 "Please select brands that you would like."
        categorical [1 .. ]
        {
            _1 "Nike",
            _2 "Adidas",
            _3 "Reebok",
            _4 "Sparx",
            _5 "LeeCooper"
        };
    End Metadata

    Routing(Web)
        Q001.Categories[{_1}].Label.Insert["ins"] = Brand
        Q001.Ask()
    End Routing

# Text Insertion - Categorical
    Metadata(en-US, Question, label)     
        S1 "What is your name?" text <br/>{#N2};

        S2 "How old are you?" long [1 .. 100] <br/>{#N2};

        S3 "Are you a college graduate? <br/>{#N2}"
        categorical [1 .. 1]
        {
            _1 "Yes",
            _2 "No"
        };

        PageS1_S2 "" page
        (
            S1, 
            S2,
            S3
        );

        N2 "Which decade you born in, select the nearest decade? <br/> (e.g., if you born between 1980 to 1984 then use 1980, if you born in 1985 to 1989 then use 1990)"
        long [1950 .. 2020 step 10];
    End Metadata

    Routing(Web)
        N2.Ask()

        PageS1_S2.Ask()
    End Routing

# Text Insertion - Loop
    Metadata(en-US, Question, label)    
        TeaList define
        {
            Assam,
            Darjeeling,
            LapsangSouchong "Lapsang Souchong",
            Gunpower,
            Puerh,
            EarlGrey "Earl Grey",
            Green,
            OrangePekoe "Orange Pekoe",
            FruitHerbal "Fruit/Herbal"
        };
 
        TeaLoop "Liking of teas" loop
        {
            use TeaList
        } fields
        (
            Drinks "Would you say you like {@}?" categorical [1..1]
            {
                Yes "Yes I like {@}",
                No "No I don't like {@}"
            };
            WhyLike "Why do you say that about {@}?" Text;
        ) expand;
    End Metadata

    Routing(Web)
        TeaLoop[..].Ask()
    End Routing

# Terminate
    Metadata(en-US, Question, label)      
        Q001 "Please select brands that you would like."
        categorical [1 .. ]
        {
            _1 "Nike",
            _2 "Adidas",
            _3 "Reebok",
            _4 "Sparx",
            _5 "LeeCooper"
        };
    End Metadata

    Routing(Web)
        Q001.Categories[{_1}].Label.Insert["ins"] = Brand
        Q001.Ask()

        If ContainsAny(Q001, {_2}) Then
            IOM.Terminate()
        End If
    End Routing