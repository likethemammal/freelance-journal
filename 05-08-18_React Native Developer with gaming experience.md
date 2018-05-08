# React Native Developer with gaming experience

- **Dates:** 4/23/18 - 5/7/18
- **Estimate:** About a week
- **Job Description:** [Upwork PDF](upwork_job_details_1.pdf)
- **Submitted Proposal:** [Upwork Cover Letter](05-08-18_cover-letter.md)

**tldr:** Used Upwork to get my first freelance job. Made a Breakout-like game in React Native. Spent days fiddling with RN physics libraries and game engines until landing on Matter.js. Ended up animating with Javascript, not Animated. Used CodeSandbox to quickly iterate and demo progress. Struggled with production build, but took a day off and got it figured out. Classic React Native fun and complexity.

### Summary

#### Starting the job

Was given a description and mockups for a simple "pong-like" game (mechanically more like Breakout) in React Native. After applying, the client and I talked about the mockups, my interest level, a time estimate, and some specific considerations. They updated the job description from the conversation and then I got access to the repo I would push my code to.

I first setup the basic React Native codebase, which includes getting all the Android APIs. And then I setup an online web playground for the project on CodeSandbox using react-native-web. This would allow quicker iteration than using a compiler and emulator, and it'd make it easy to share and test my progress.

Before I started, I thought out how I would animate the balls on screen and handle collision with the paddles, since that was most of what this game was. For a bit I toyed with the idea of animating the balls using React Native's Animation pattern, but I would have to know the exact speed, length, and speed fall off of each change in direction each ball would have. Basically creating a physics engine specifically for `Animated`. Waay too much work for a one week freelance project.

#### Finding a physics engine

Realizing that, I was worried that creating an animation loop manually and animating using Javascript would be horribly slow. There was also the possibility of using some react-canvas library that imports HTML Canvas, so I could just use that instead of animating RN View's.

Either way, I would have to use JS, so I set out to find a JS physics library that works with React Native. Surprisingly few options. ReactGameKit is the go-to game creation framework for React and React Native, but it had more going on than what I wanted. react-native-game-engine seemed promising and react-native-collidable also sounded like it would work for my use case.

I decided against react-native-collidable because I was worried I'd need more specific control over the physics, and I didnt want to be restricted to collisions. After fiddling with react-native-game-engine and ReactGameKit for multiple days I wasnt any closer to have React Native working with a physics engine.

The ReactGameKit docs mentioned that it uses Matter.js to handle physics bodies. This tipped me to the fact that Matter.js doesnt depend on the HTML canvas element to do its physics, and that it could run in React Native. Matter.js is a very straightforward and simple physics library for working with a variety of polygons and forces, and exactly what I wanted. This would allow me to create an invisible game world that handled the physics and just render the result using React Native.

This ended up working great. The performance of manually moving the x and y of a View across screen was surprisingly smooth. The only glaring caveat was that Matter.js uses a shape's center coordinates to position x and y, while React Native and the Web use the top left corner. This was confusing for a while, as collision detection looked like it wasnt working. After turning on debug mode, and realizing the difference in their positions, it was a quick fix.

#### The fun parts

The rest of the project was the paradise of playing with physics and adding game elements. Only took me 2 days after this point to get the game to a finished state.

Spent the next day or 2 polishing it until it perfectly matched the mockups. After it matched, I imported the code back into the basic RN codebase I had setup and started integrating my work. It was mostly just fixing minor syntax issues, but really react-native-web did its job perfectly.

#### Production build

After getting the game running in the emulator, I moved to getting the production build working. This became the biggest blocker for the rest of the project. Spent a day debugging into the darkness. Realizing it could take several days and that my deadline was approaching, I packaged up all my work so far, including the CodeSandbox demo, and sent it to the client. I mentioned I'd be debugging the production build for a few days, but really the project was finished. He appreciated what he saw in the demo.

After a day off, I decided I'd make a new blank RN project and get that build working, then I'd just move my code over to that codebase. Got the build working with a sample project, moved my code, got the build working again, but the app instantly crashes. Debug line-per-line, still no fix, and now the old blank code isnt working. After making another blank RN project, I realized that I had previously changed the name of the App at some point, assuming I had changed it in all the right places. I remembered reading something a while ago about how this isnt so straightforward in RN, so I reverted my App name changes and the crashes were fixed.

Messaged the client that I had fixed that last issue, updated the README with production build instructions, and pushed the code to the repo.

