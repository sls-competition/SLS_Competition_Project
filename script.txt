let users = [];
let currentUser = null;

// Load existing data from data.json
fetch('data.json')
    .then(response => response.json())
    .then(data => {
        users = data.users;
    });

// Update user score
function updateUserScore(username, points) {
    const user = users.find(u => u.username === username);
    if (user) {
        user.score = (user.score || 0) + points;
    }
}

// Signup function
function signup(username, password) {
    if (!users.find(u => u.username === username)) {
        users.push({ username, password, score: 0 });
        alert("Signup successful!");
        return true;
    } else {
        alert("Username already taken.");
        return false;
    }
}

// Login function
function login(username, password) {
    const user = users.find(u => u.username === username && u.password === password);
    if (user) {
        currentUser = user;
        alert("Login successful!");
        return true;
    } else {
        alert("Invalid credentials!");
        return false;
    }
}

// Password recovery
function recoverPassword(username) {
    const user = users.find(u => u.username === username);
    if (user) {
        alert(`Your password is: ${user.password}`);
    } else {
        alert("Username not found.");
    }
}

// Function to track mood and update score
function trackMood(mood) {
    const points = 1; // Points for mood tracking
    if (currentUser) {
        updateUserScore(currentUser.username, points);
        alert("Mood tracked successfully!");
    }
}

// Function to save journal entry and update score
function saveJournal(entry) {
    const points = 2; // Points for journaling
    if (currentUser) {
        updateUserScore(currentUser.username, points);
        alert("Journal entry saved!");
    }
}
