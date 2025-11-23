#All defined functions to keep it tidy

def main():
    while True:
        #Asks the player for their player id. no char limits as their could be billions of players
        global playerID
        playerID = input("What is your player ID? Your ID will only contain numbers.\nPlayer ID: ")
        if (playerID.isalpha()):
            #loop to see if the id contains any illegal characters
            #if it does then it will loop back and ask for their input again
            #if it does not, then the program will continue as normal
            print("Invalid input, please try again.")
            continue
        else:
            play()
            #going to the next function if checks have been passed
            return

def play():
    while True:
        #asks player for playcount, again checking if it meets requirements
        global playCount
        playCount = int(input("How many games did you play? Must be between 5 and 10 (inclusive).\nGames Played: "))
        if playCount < 5 or playCount > 10:
            print("Invalid input, please try again.")
            continue
        else:
            data()
            #continue
            return

def data():
    #defining the lists that will be needed
    global scores
    scores = []
    global times
    times = []
    for i in range(playCount):
        #using playcount to ask the correct amount of times for info
        newScore = input("What was your score?\nScore: ")
        #appending score to scores list
        scores.append(newScore)
        while True:
            #checking if playtime is valid
            newTime = float(input("What was your playtime in whole minutes? Playtime should be between 5 and 60 minutes (inclusive)\nPlaytime: "))
            if newTime < 5 or newTime > 60:
                print("Those times are impossible, please try again.")
                continue
            else:
                #rounding playtime to the nearest whole number as people may input a decimal
                newTime = round(newTime)
                #appending time to times list
                times.append(newTime)
                break
    user()

def user():
    #sorting the scores from highest to lowest to get top score
    scores.sort(reverse=True)
    #getting top score from position 0 in list
    topScore = scores[0]
    #getting average time by getting sum and dividing by playcount
    avgTime = sum(times)/playCount
    #telling the user their info of the last play
    print(f"Hello, {playerID}.\nYour top score: {topScore}\nYour average time: {avgTime}")
    #creating unique file for each users play data
    #using append in case someone plays multiple times on different occasions
    f = open(f"{playerID}.txt", "a")
    f.write(f"Player ID: {playerID}\nTop score: {topScore}\nAverage time: {avgTime}\n\nScores: {scores}\nTimes: {times}\n\n")
    
main()