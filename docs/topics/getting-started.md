package com.example.urdubaitbazi

import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    private lateinit var userCoupletInput: EditText
    private lateinit var submitButton: Button
    private lateinit var coupletDisplay: TextView
    private lateinit var responseText: TextView

    // Sample dataset for Urdu couplets. In a real app, this would be a much larger dataset or fetched from a local database.
    private val couplets = listOf(
        "دل ہی تو ہے نہ سنگ و خشت درد سے بھر نہ آئے کیوں",
        "دیتے ہیں بادہ ظرف قدح خوار دیکھ کر",
        "عمر بھر دیکھا کیے مرنے کا منظر ہم نے",
        "سر پیٹتے ہیں کب تک دل کو بہلائیں کہاں تک",
        "ہم ہیں مشتاق اور وہ بیزار یا الہی یہ ماجرا کیا ہے"
    )

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        userCoupletInput = findViewById(R.id.userCoupletInput)
        submitButton = findViewById(R.id.submitButton)
        coupletDisplay = findViewById(R.id.coupletDisplay)
        responseText = findViewById(R.id.responseText)

        // Set up initial couplet
        coupletDisplay.text = "Let's start the Baitbazi! Enter your couplet."

        // Handle submit button click
        submitButton.setOnClickListener {
            val userCouplet = userCoupletInput.text.toString().trim()
            if (userCouplet.isNotEmpty()) {
                // Check if user input is valid (you can add more validation here)
                coupletDisplay.text = userCouplet
                // Call function to get the robot's response
                val robotCouplet = getRobotCouplet(userCouplet)
                responseText.text = "Robot's response: $robotCouplet"
            }
        }
    }

    // Simple logic to fetch a couplet that matches the last letter of the user's couplet
    private fun getRobotCouplet(userCouplet: String): String {
        // Get the last character of the user's couplet
        val lastChar = userCouplet.lastOrNull()?.toLowerCase()

        // Find a couplet that starts with the same letter
        for (couplet in couplets) {
            if (couplet.firstOrNull()?.toLowerCase() == lastChar) {
                return couplet
            }
        }
        // If no match is found, return a default response
        return "Sorry, no matching couplet found."
    }
}
