# Tips_04_02_SpeechSynthesizer_End
The end state for the speech synthesizer example

It's sometimes nice to add a little sound to your applications, and even better to add a voice. Outside Siri, you can use a cool and simple <code>AVFoundation</code> API to make iOS devices talk. Let's learn how to use the Speech synthesizer.
<a href="http://bit.ly/SpeechSynthBegin">Download the starter file</a>. I've made an app for you that has a text field, a button and a segue to a table view we'll discuss a little later.
Open the <code>ViewController,swift</code> file. Find the <code>speak</code> action. We'll need to get a string from the text field. So add the following code to get the text if the field has a value:

[code]
if let speechText = speakingText.text{
}
[/code]
You'll need two objects: a synthesizer object and a speech utterance. But before you do, make sure you have imported <code>AVFoundation</code>.

[code]import AVFoundation[/code]
I'll add the synthesizer with the <code>AVSpeechSynthesizer</code> class

[code]
let synth = AVSpeechSynthesizer()
let speech = AVSpeechUtterance(string: speechText)
synth.speak(speech)
[/code]
That's it. Set your simulator to iPhone 8 Plus. Build and run the app. Type in some phrase, like
<em>I could use a good pizza right now.</em>
Tap the <strong>Speak!</strong> Button.

 

[wpvideo PH1TMKMh]

Your simulator speaks!!

Of course that's not the only method you have at your disposal. You can easily change the voice as well. Voices are a localization in pronunciation. Some languages will have more than one available pronunciation. I set up the app to list all the voices and their language combinations on a table view and then the user can select the voice and accent.

You'll use the <code>AVSpeechSynthesisVoice</code> class for this. There is a class method that returns an array of voices. I'll use this for my model for the table

[code]
let voices = [AVSpeechSynthesisVoice.speechVoices()] //list of voices
[/code]

Head down the code to the <code>tableview.dequeue</code> method. Remove what I have their now. All the voices have, names, Identifiers and languages. Names are only indication if they are male or female voices until you hear them. You use the name property. Since these properties are strings. we can assign the name directly to the text label and the language to the detail text label of the table cell.

[code]
cell.textLabel?.text = voice.name
cell.detailTextLabel?.text = voice.language
[/code]
When a language is selected I’ll send that voice back from the table and dismiss the table. I set up the delegation for you. In <code>didselect</code>, uncomment out the two lines. If you don't understand what I’m doing here take a look at the <a href="http://bit.ly/swiftDelegation">delegates and data sources course in the library</a>.
Back in <code>ViewController</code>, you’ll see I have the delegate method defined to transfer the voice to a variable. All you need to do is assign the voice with the action to the variable.

[code]
Speech.voice = speechVoice
[/code]
Now run. Tap voice and then pick another voice. Try the voice.

 

[wpvideo aM3cxYSC]

Play around with this. Of course,  voices are more for localization than entertainment. There’s more to the API, but with these basics you can make your app talk.
