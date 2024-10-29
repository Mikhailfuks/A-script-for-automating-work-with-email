// Import Nodemailer package
const nodemailer = require('nodemailer');

// Create a transporter object using SMTP configuration
const transporter = nodemailer.createTransport({
    host: 'smtp.example.com', // SMTP server address
    port: 587, // SMTP port
    secure: false, // true for 465, false for other ports
    auth: {
        user: 'your-email@example.com', // your email
        pass: 'your-email-password' // your email password or application-specific password
    }
});

// Function to send an email
const sendEmail = async (to, subject, text, html) => {
    try {
        // Email options
        const mailOptions = {
            from: '"Your Name" <your-email@example.com>', // sender address
            to, // recipient address
            subject, // Subject line
            text, // plain text body
            html // html body
        };

        // Send mail
        const info = await transporter.sendMail(mailOptions);
        console.log('Message sent: %s', info.messageId);
    } catch (error) {
        console.error('Error sending email: ', error);
    }
};

// Usage example
const recipientEmail = 'recipient@example.com';
const subject = 'Automated Email';
const text = 'Hello, this is an automated email from your Node.js application!';
const html = '<p>Hello, this is an <strong>automated</strong> email from your <em>Node.js</em> application!</p>';

// Send the email
sendEmail(recipientEmail, subject, text, html);
