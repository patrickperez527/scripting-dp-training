# Day 2 Assesment Answers

# Metadata 
    Metadata(fil-PH, Question, Label)
        I1 "Welcome to Survey Health Care! This survey will take you about 5 minutes. As always, your individual survey responses are protected by our Privacy Policy."
            info;

            S2 "Please indicate your gender:"
            categorical [1..1]
            {
                _1 "Male",
                _2 "Female"
            };

            S3 "Which brands are you aware of?"
            categorical [1..]
            {
                _1 "Nike",
                _2 "Adidas",
                _3 "Reebok",
                _4 "Sparx",
                _5 "LeeCooper",
                _6 "Others" fix,
                _7 "None of these" fix exclusive
            } rot;

            S4 "Would you consider these brands in future?"
            categorical [1..]
            {
                _1 "Nike",
                _2 "Adidas",
                _3 "Reebok",
                _4 "Sparx",
                _5 "LeeCooper",
                _6 "Others" fix,
                _7 "None of these" fix exclusive
            };

            Q1 "Do you or does any member of your household work in any of the following occupations?"
            categorical [1..]
            {
                _1 "Advertising",
                _2 "Market Research",
                _3 "Marketing",
                _4 "Journalism",
                _6 "Public Relations",
                _7 "Healthcare Manufacturer",
                _8 "None of these" fix exclusive
            } ran;

            Q2 "Where have you shopped for office supplies in the past 6 months? (Select all that apply)"
            categorical [1..]
            {
                _1 "Grocery store",
                _2 "Convenience store",
                _3 "Club stores (like Sam's Club, Costco, BJ's)",
                _4 "Discount stores (like Target, Walmart, Kmart)",
                _5 "Drug stores (like Walgreen's CVS)",
                _6 "Office Superstores (like Office Max, Office Depot, Staples)",
                _7 "Dollar stores (like Dollar General, Dollar Tree)",
                _8 "Catalogs",
                _9 "Online (like Amazon, Staples.com)",
                _999 "Other: Please Specify" other fix
            } ran;

            Q3 "Where do you shop <u>most often</u> for office supplies? (Select one)"
            categorical [1..1]
            {
                _1 "Grocery store",
                _2 "Convenience store",
                _3 "Club stores (like Sam's Club, Costco, BJ's)",
                _4 "Discount stores (like Target, Walmart, Kmart)",
                _5 "Drug stores (like Walgreen's CVS)",
                _6 "Office Superstores (like Office Max, Office Depot, Staples)",
                _7 "Dollar stores (like Dollar General, Dollar Tree)",
                _8 "Catalogs",
                _9 "Online (like Amazon, Staples.com)",
                _999 "{#Q2._999}" fix
            } ran;

            Q4 "Where do you shop <u>least often</u> for office supplies? (Select one)"
            categorical [1..1]
            {
                _1 "Grocery store",
                _2 "Convenience store",
                _3 "Club stores (like Sam's Club, Costco, BJ's)",
                _4 "Discount stores (like Target, Walmart, Kmart)",
                _5 "Drug stores (like Walgreen's CVS)",
                _6 "Office Superstores (like Office Max, Office Depot, Staples)",
                _7 "Dollar stores (like Dollar General, Dollar Tree)",
                _8 "Catalogs",
                _9 "Online (like Amazon, Staples.com)",
                _999 "{#Q2._999}" fix
            } ran;

            Q5 "At what age do you plan to retire?"
            categorical [1..1]
            {
                _1 "Between the ages 50-54",
                _2 "Between the ages 55-59",
                _3 "Between the ages 60-65",
                _4 "Over 65",
                _5 "Don't plan to retire",
                _6 "Already retired",
                _7 "Dont know" DK,
                _8 "Refused" REF
            };

            T1 "Whats your favorite Brand? <br/> (Please be honest)"
            text;

            T2 "Do you own a car? If yes which Brand it is?"
            text [1..10];

            N1 "What is your age? (Please state your exact age)"
            long [1 .. 100, ^50 .. 60];

            N2 "Which decade you born in, select the nearest decade? <br/> (e.g., if you born between 1980 to 1984 then use 1980, if you born in 1985 to 1989 then use 1990)"
            long [1950 .. 2020 step 10];

            N3 "What is the percentage you got in SSC?"
            double [1 .. 100]
            scale(2);

            L1 "At which touchpoints did you encounter <u>fashion-ready-to-wear</u> brands in the last 3 months?" loop
            {
                _1 "In a paper magazine or newspaper",
                _2 "Outdoors or while travelling (e.g. poster, bus stop…)",
                _3 "On social media or a messaging app (e.g. WhatsApp, Facebook, Instagram, LinkedIn, Twitter, Snapchat, TikTok)",
                _4 "While searching, browsing or reading a website online (not social media)",
                _5 "While browsing or reading a mobile app (not social media)",
                _6 "When shopping or browsing shopping sites online (e.g. Amazon)",
                _7 "On an online video platform (e.g. YouTube, Vimeo)",
                _8 "From a friend, family or someone else I know"
            } ran fields -
            (
                "scale" ""
                categorical [1..1]
                {
                    _1 "Yes, I recognized a fashion ready-to-wear brand",
                    _2 "No, I did not recognize a fashion ready-to-wear brand"
                };

            ) expand grid;

            Loop_L12 "" loop
            {
                _1 "Nike",
                _2 "Adidas",
                _3 "Reebok",
                _4 "Sparx",
                _5 "LeeCooper"
            } fields -
            (
                L12 "Please select your option about brands <br/> <b>{@}</b>"
                categorical [1..1]
                {
                    _1 "Excellent",
                    _2 "Good",
                    _3 "Ok",
                    _4 "Bad",
                    _5 "Very Bad"
                };

            ) expand;

            Loop_L2 "" loop
            {
                _1 "Nike",
                _2 "Adidas",
                _3 "Reebok",
                _4 "Sparx",
                _5 "LeeCooper"
            } fields -
            (
                L12 "How has your experience at each touchpoint changed your attitude towards <b>{@}</b>?" loop
                {
                    _1 "In a paper magazine or newspaper",
                    _2 "Outdoors or while travelling (e.g. poster, bus stop…)",
                    _3 "On social media or a messaging app (e.g. WhatsApp, Facebook, Instagram, LinkedIn, Twitter, Snapchat, TikTok)",
                    _4 "While searching, browsing or reading a website online (not social media)",
                    _5 "While browsing or reading a mobile app (not social media)",
                    _6 "When shopping or browsing shopping sites online (e.g. Amazon)",
                    _7 "On an online video platform (e.g. YouTube, Vimeo)",
                    _8 "From a friend, family or someone else I know"
                } ran fields -
                (
                    slice ""
                    categorical [1..1]
                    {
                        _1 "Strongly negative = -5",
                        _2 "-4",
                        _3 "-3",
                        _4 "-2",
                        _5 "-1",
                        _6 "-4",
                        _7 "No effect on my attitude = 0",
                        _8 "+1",
                        _9 "+2",
                        _10 "+3",
                        _11 "+4",
                        _12 "Strongly positive = +5"
                    };

                );

            ) expand grid;

            Outro "Thank you for taking this survey!"
            info;
    End Metadata

# Routing
    Routing(Web)
        I1.Show()
        
        S2.Ask()
        
        S3.Ask()
        
        If ContainsAny(S3, {_2}) Then
            S4.Categories.Order = orderConstants.oCustom
            S4.Categories = {_2, _1, _4, _3, _6, _7}
        Else 
            S4.Categories.Order = orderConstants.oRandomize
        End If
        
        S4.Ask()
        
        Q1.Ask()
        
        If ContainsAny(Q1, {_1, _3, _4}) Then
            Q2.Ask()
        End If
        
        Q3.Categories.Filter = Q2.Response
        
        'Q3 will only ask a question if Q2 is answered
        If AnswerCount(Q2) > 0 Then
            Q3.Ask()
        End If
        
        Q4.Categories = {}
        Q4.Categories = Q2.Response - Q3.Response
        
        'Added the logical operator "AND" so the Q4 will only ask a question if Q3 is answered
        If Q4.Categories.Count > 0 AND AnswerCount(Q3) > 0 Then
            If (Q4.Categories.Count) = 1 Then
                Q4.Response = Q4.Categories
                'If IOM.Info.IsDebug Then Q4.Show()
            Else
                Q4.Ask()
            End If
        End If
        
        If ContainsAny (Q1, {_8}) Then
            Q5.Ask()
        End If
        
        T1.Style.Control = ControlTypes.ctSingleLineEdit
        T1.Ask()
        
        T2.Style.Control = ControlTypes.ctSingleLineEdit
        T2.Ask()
        
        N1.Ask()
        
        N2.Ask()
        
        N3.Ask()
        
        L1.Ask()
        
        Loop_L12[..].Ask()
        
        Loop_L2[..].Ask()
        
        Outro.Show()
    End Routing