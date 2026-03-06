Here are some thoughts on a prototype for the website:
1. The landing pages shows the information in @01-intro.md. It contains a video carousel (see commented text in 01-intro.md).
2. The basics perhaps appear immediately below the intro (visible only when the user scrolls down), or appear on a different page.
3. Perhaps the safety page should contain an interactive element, the "safety checker":
   * (Similar to [this](https://clusterheadaches.co/treatment-blockers):) You can make a list of all the medications/drugs you’re on (+ whether you have cardiovascular problems), and:
     * You get an estimate of the risk level. E.g., 4 tiers:
         * [High risk -- lithium] Don’t do DMT, seizure risk
         * [Moderate risk -- MAOIs] Check with your doc + read resources on serotonin syndrome + always be with a sitter
         * [Low risk -- SNRIs / SSRIs / others] Check with your doc + read resources on serotonin syndrome
         * [Low risk -- cardiovascular] Check with your doc + don’t have triptans in your system when you take DMT
       * (Maybe?) The website generates a “personalized” (tier-dependent + with the list of meds) message for your doc that you can print out 
       * Obviously, we cannot list all medications. What I suggest we do: Have (1) a black list of common risky meds,  (2) a white list of common non-risky meds, (3) a catch-all for anything that’s not on either list, which triggers a “do research or check with your doc” warning.
4. That said, the safety checker shouldn't be a distraction. Only implement it if it feels like it doesn't trade off against other aspects or features.
5. We could get creative with hidden blocs, highlighted elements, etc, that make the website easier to read