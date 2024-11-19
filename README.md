CREATE DATABASE WorkoutTracker;
USE WorkoutTracker;


CREATE TABLE User (
  UserID INT AUTO_INCREMENT PRIMARY KEY,
  FirstName VARCHAR(50) NOT NULL,
  LastName VARCHAR(50) NOT NULL,
  Email VARCHAR(100) UNIQUE NOT NULL,
  Age INT CHECK (Age > 0),
  FitnessGoal VARCHAR(255)
);

CREATE TABLE WorkoutName (
  WorkourID INT AUTO_INCREMENT PRIMARY KEY,
  WorkoutName VARCHAR(100) NOT NULL,
  Duration INT NOT NULL CHECK (Duration > 0)
  DifficultyLevel VARCHAR(50 NOT NULL,
  Description TEXT
);

CREATE TABLE ExerciseLog (
  LogID INT AUTO_INCREMENT PRIMARY KEY,
  UserID INT NOT NULL,
  WorkoutID INT,
  Date DATE NOT NULL,
  Duration INT NOT NULL CHECK (Duration > 0),
  Notes TEXT,

  FOREIGN KEY (UserID) REFERENCES User(UserID)
    ON DELETE CASCADE,
  FOREIGN KEY (WorkoutID) REFERENCES WorkoutName(WorkoutID)
    ON DELETE SET NULL
);

CREATE INDEX idx_UserEmail ON User(Email);                
CREATE INDEX idx_WorkoutName ON WorkoutName(WorkoutName);  
CREATE INDEX idx_LogDate ON ExerciseLog(Date);             


INSERT INTO User (FirstName, LastName, Email, Age, FitnessGoal)
VALUES
('Kyle', 'Keay', 'Kkeay@example.com', 30, 'Lose weight'),
('Steve', 'Austin', 'stonecold@example.com', 25, 'Build muscle'),
('Jimmy', 'Dean', 'sausage@example.com', 35, 'Improve endurance');


INSERT INTO WorkoutName (WorkoutName, Duration, DifficultyLevel, Description)
VALUES
('Cardio Blast', 30, 'Intermediate', 'A high-energy cardio workout.'),
('Strength Training', 45, 'Advanced', 'A workout focusing on muscle strength.'),
('Yoga Flow', 60, 'Beginner', 'A relaxing yoga session.');


INSERT INTO ExerciseLog (UserID, WorkoutID, Date, Duration, Notes)
VALUES
(1, 1, '2024-11-15', 30, 'Felt great after the workout!'),
(2, 2, '2024-11-16', 45, 'Pushed myself harder today.'),
(3, 3, '2024-11-17', 60, 'Very relaxing session.');


CREATE USER 'workout_user'@'localhost' IDENTIFIED BY 'securepassword';
GRANT ALL PRIVILEGES ON WorkoutTracker.* TO 'workout_user'@'localhost';


FLUSH PRIVILEGES;
