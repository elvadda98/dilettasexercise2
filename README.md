<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday Terms</h1>
            <p>Test your knowledge of these English terms!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>oven</h3>
                    <p><strong>Definition:</strong> An enclosed compartment for cooking and heating food.</p>
                    <p><strong>Usage:</strong> Common kitchen appliance for baking, roasting, and heating.</p>
                    <p class="example"><strong>Example:</strong> "I baked the cake in the oven for 45 minutes."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>shame</h3>
                    <p><strong>Definition:</strong> A painful feeling of humiliation or distress caused by wrong behavior.</p>
                    <p><strong>Usage:</strong> Also used to express disappointment (e.g., "What a shame!").</p>
                    <p class="example"><strong>Example:</strong> "He felt deep shame after lying to his parents."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>renovate</h3>
                    <p><strong>Definition:</strong> To restore something to a good state of repair; to modernize.</p>
                    <p><strong>Usage:</strong> Commonly used for buildings, houses, or rooms.</p>
                    <p class="example"><strong>Example:</strong> "We plan to renovate the kitchen next month."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>deal</h3>
                    <p><strong>Definition:</strong> An agreement or arrangement, especially in business.</p>
                    <p><strong>Usage:</strong> Also means to cope with or handle a situation.</p>
                    <p class="example"><strong>Example:</strong> "We made a deal to share the profits equally."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>pros and cons</h3>
                    <p><strong>Definition:</strong> The advantages and disadvantages of something.</p>
                    <p><strong>Usage:</strong> Used when evaluating options or making decisions.</p>
                    <p class="example"><strong>Example:</strong> "Let's list the pros and cons before making a decision."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>pretty</h3>
                    <p><strong>Definition:</strong> Attractive in a delicate way; also used as an adverb meaning 'quite' or 'fairly'.</p>
                    <p><strong>Usage:</strong> Can describe appearance or degree.</p>
                    <p class="example"><strong>Example:</strong> "She's pretty sure she left her keys on the table."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>move</h3>
                    <p><strong>Definition:</strong> To change position or location; to go to a different place.</p>
                    <p><strong>Usage:</strong> Also means to change residence or make a strategic action.</p>
                    <p class="example"><strong>Example:</strong> "We need to move these boxes to the storage room."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>lawyer</h3>
                    <p><strong>Definition:</strong> A person who practices or studies law; an attorney.</p>
                    <p><strong>Usage:</strong> Professional who provides legal advice and representation.</p>
                    <p class="example"><strong>Example:</strong> "You should consult a lawyer before signing the contract."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>back off</h3>
                    <p><strong>Definition:</strong> To withdraw from a confrontation; to stop being involved.</p>
                    <p><strong>Usage:</strong> Phrasal verb used in conflicts or difficult situations.</p>
                    <p class="example"><strong>Example:</strong> "I told him to back off and give me some space."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>scam</h3>
                    <p><strong>Definition:</strong> A dishonest scheme; a fraud.</p>
                    <p><strong>Usage:</strong> Describes deceptive practices to obtain money or information.</p>
                    <p class="example"><strong>Example:</strong> "The email turned out to be a phishing scam."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>wheels</h3>
                    <p><strong>Definition:</strong> Circular objects that rotate on an axle, used for transportation.</p>
                    <p><strong>Usage:</strong> Also slang for a car or vehicle.</p>
                    <p class="example"><strong>Example:</strong> "I need to get new wheels for my bicycle."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">oven</span>
                    <span class="word-option">shame</span>
                    <span class="word-option">renovate</span>
                    <span class="word-option">deal</span>
                    <span class="word-option">pros and cons</span>
                    <span class="word-option">pretty</span>
                    <span class="word-option">move</span>
                    <span class="word-option">lawyer</span>
                    <span class="word-option">back off</span>
                    <span class="word-option">scam</span>
                    <span class="word-option">wheels</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="oven" onclick="selectMatch(this)">oven</div>
                    <div class="match-item" data-word="shame" onclick="selectMatch(this)">shame</div>
                    <div class="match-item" data-word="renovate" onclick="selectMatch(this)">renovate</div>
                    <div class="match-item" data-word="deal" onclick="selectMatch(this)">deal</div>
                    <div class="match-item" data-word="pros and cons" onclick="selectMatch(this)">pros and cons</div>
                    <div class="match-item" data-word="pretty" onclick="selectMatch(this)">pretty</div>
                    <div class="match-item" data-word="move" onclick="selectMatch(this)">move</div>
                    <div class="match-item" data-word="lawyer" onclick="selectMatch(this)">lawyer</div>
                    <div class="match-item" data-word="back off" onclick="selectMatch(this)">back off</div>
                    <div class="match-item" data-word="scam" onclick="selectMatch(this)">scam</div>
                    <div class="match-item" data-word="wheels" onclick="selectMatch(this)">wheels</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What is an "oven"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of vehicle</div>
                    <div class="option" onclick="selectOption(this, true)">An enclosed compartment for cooking</div>
                    <div class="option" onclick="selectOption(this, false)">A legal document</div>
                    <div class="option" onclick="selectOption(this, false)">A type of scam</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What does "shame" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A feeling of pride</div>
                    <div class="option" onclick="selectOption(this, true)">A painful feeling of humiliation</div>
                    <div class="option" onclick="selectOption(this, false)">A business agreement</div>
                    <div class="option" onclick="selectOption(this, false)">A cooking method</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "renovate" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To destroy something</div>
                    <div class="option" onclick="selectOption(this, true)">To restore to a good state</div>
                    <div class="option" onclick="selectOption(this, false)">To move to a new location</div>
                    <div class="option" onclick="selectOption(this, false)">To make a business deal</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What is a "deal"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of oven</div>
                    <div class="option" onclick="selectOption(this, true)">An agreement or arrangement</div>
                    <div class="option" onclick="selectOption(this, false)">A feeling of shame</div>
                    <div class="option" onclick="selectOption(this, false)">A renovation project</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What are "pros and cons"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Legal professionals</div>
                    <div class="option" onclick="selectOption(this, true)">Advantages and disadvantages</div>
                    <div class="option" onclick="selectOption(this, false)">Types of scams</div>
                    <div class="option" onclick="selectOption(this, false)">Kitchen appliances</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "pretty" mean as an adverb?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Very ugly</div>
                    <div class="option" onclick="selectOption(this, true)">Quite or fairly</div>
                    <div class="option" onclick="selectOption(this, false)">Extremely expensive</div>
                    <div class="option" onclick="selectOption(this, false)">Completely wrong</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "move" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To stay in one place</div>
                    <div class="option" onclick="selectOption(this, true)">To change position or location</div>
                    <div class="option" onclick="selectOption(this, false)">To create a scam</div>
                    <div class="option" onclick="selectOption(this, false)">To feel shame</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: Who is a "lawyer"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A kitchen appliance repair person</div>
                    <div class="option" onclick="selectOption(this, true)">A person who practices law</div>
                    <div class="option" onclick="selectOption(this, false)">Someone who creates scams</div>
                    <div class="option" onclick="selectOption(this, false)">A car mechanic</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "back off" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To move forward aggressively</div>
                    <div class="option" onclick="selectOption(this, true)">To withdraw from a confrontation</div>
                    <div class="option" onclick="selectOption(this, false)">To make a business deal</div>
                    <div class="option" onclick="selectOption(this, false)">To renovate a building</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 10: What is a "scam"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A legitimate business deal</div>
                    <div class="option" onclick="selectOption(this, true)">A dishonest scheme or fraud</div>
                    <div class="option" onclick="selectOption(this, false)">A type of oven</div>
                    <div class="option" onclick="selectOption(this, false)">A legal agreement</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 11: What are "wheels"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Legal documents</div>
                    <div class="option" onclick="selectOption(this, true)">Circular objects for transportation</div>
                    <div class="option" onclick="selectOption(this, false)">Types of shame</div>
                    <div class="option" onclick="selectOption(this, false)">Kitchen utensils</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "oven", text: "An enclosed compartment for cooking" },
            { meaning: "shame", text: "A painful feeling of humiliation" },
            { meaning: "renovate", text: "To restore to a good state" },
            { meaning: "deal", text: "An agreement or arrangement" },
            { meaning: "pros and cons", text: "Advantages and disadvantages" },
            { meaning: "pretty", text: "Attractive; or quite/fairly" },
            { meaning: "move", text: "To change position or location" },
            { meaning: "lawyer", text: "A person who practices law" },
            { meaning: "back off", text: "To withdraw from confrontation" },
            { meaning: "scam", text: "A dishonest scheme or fraud" },
            { meaning: "wheels", text: "Circular objects for transportation" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "I baked the cake in the <input type='text' class='fill-blank' data-answer='oven' placeholder='answer'> for 45 minutes.", answer: "oven" },
            { text: "He felt deep <input type='text' class='fill-blank' data-answer='shame' placeholder='answer'> after lying to his parents.", answer: "shame" },
            { text: "We plan to <input type='text' class='fill-blank' data-answer='renovate' placeholder='answer'> the kitchen next month.", answer: "renovate" },
            { text: "We made a <input type='text' class='fill-blank' data-answer='deal' placeholder='answer'> to share the profits equally.", answer: "deal" },
            { text: "Let's list the <input type='text' class='fill-blank' data-answer='pros and cons' placeholder='answer'> before making a decision.", answer: "pros and cons" },
            { text: "She's <input type='text' class='fill-blank' data-answer='pretty' placeholder='answer'> sure she left her keys on the table.", answer: "pretty" },
            { text: "We need to <input type='text' class='fill-blank' data-answer='move' placeholder='answer'> these boxes to the storage room.", answer: "move" },
            { text: "You should consult a <input type='text' class='fill-blank' data-answer='lawyer' placeholder='answer'> before signing the contract.", answer: "lawyer" },
            { text: "I told him to <input type='text' class='fill-blank' data-answer='back off' placeholder='answer'> and give me some space.", answer: "back off" },
            { text: "The email turned out to be a phishing <input type='text' class='fill-blank' data-answer='scam' placeholder='answer'>.", answer: "scam" },
            { text: "I need to get new <input type='text' class='fill-blank' data-answer='wheels' placeholder='answer'> for my bicycle.", answer: "wheels" },
            { text: "The bread needs to go in the <input type='text' class='fill-blank' data-answer='oven' placeholder='answer'> for 20 minutes.", answer: "oven" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
