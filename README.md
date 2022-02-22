# I_learned_today
A  casual blog to record things I learned on internet related to programming.


22/2/2022

In Node.js, `console.log()` is actually:
 `console.log = function (d) {
  process.stdout.write(d + '\n');
};`

source: https://nodejs.org/docs/v0.3.1/api/process.html#process.stdout
