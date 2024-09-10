---
layout: default
title: XSS - Testes
parent: XSS
grand_parent: Templates
---


<!DOCTYPE html>
<html>
<head>
    <title>Simple XSS Example</title>
</head>
<body>
    <h2>Feedback Form</h2>
    <form>
        <label for="feedback">Enter your feedback:</label><br>
        <input type="text" id="feedback" name="feedback"><br>
        <button type="button" onclick="submitFeedback()">Submit</button>
    </form>

    <script>
        function submitFeedback() {
            var feedback = document.getElementById('feedback').value;
            document.getElementById('display').innerHTML = 'Your feedback: ' + feedback;
        }
    </script>

    <div id="display"></div>
</body>
</html>
