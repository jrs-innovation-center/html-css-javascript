var marked = require('npm:marked')

var Sandbox = require('./shared/sandbox')

module.exports = (h, update) => {
  function component (props) {
    var state = props
    state.canRun = true
    state.code = `
var container = output()
var canvas = document.createElement('canvas')
var w = 400
var h = 400
var size = 10

var snake = []
var food = {}

var direction = 'right'

// TODO: Step 3 - declare score variable

// set height and width
canvas.setAttribute('height', h)
canvas.setAttribute('width', w)

// add to the container
container.appendChild(canvas)

// set canvas to 2d
var ctx = canvas.getContext("2d")

function paint () {
    // paint board
    ctx.fillStyle = 'white'
    ctx.fillRect(0, 0, w, h)
    ctx.strokeStyle = 'black'
    ctx.strokeRect(0, 0, w, h)

    var head = snake[0]

    // TODO: Step 1 - reset game if snake its border or itself

    if (direction === 'right') head.x = head.x + 1
    else if (direction === 'left') head.x = head.x - 1
    else if (direction === 'up') head.y = head.y - 1
    else if (direction === 'down') head.y = head.y + 1

    // TODO: Step 2 - eat food

    snake.unshift(tail)


    snake.forEach(paintCell)

    paintCell(food)

    // TODO: Step 6 - paint score

    setTimeout(paint, 60)
}

function paintCell (c) {
    ctx.fillStyle = 'blue'
    ctx.fillRect(c.x * size, c.y * size, size, size)
    ctx.strokeStyle = 'white'
    ctx.strokeRect(c.x * size, c.y * size, size, size)
}

function createSnake () {
    return times(5, function (i) {
        return { x: i, y: 0 }
    })
}

function createFood () {
    return {
        x: random(size, w),
        y: random(size, h)
    }
}

keyEvent(function (code) {
  if (code === 37) direction = 'left'
  else if (code === 38) direction = 'up'
  else if (code === 39) direction = 'right'
  else if (code === 40) direction = 'down'
})

function init () {
  // TODO: Step 5 - reset score
  direction = 'right'
  snake = createSnake()
  food = createFood()
  paint()
}

init()
`

    function menuClick (e) {
        e.preventDefault()
        state.setRoute('menu')
    }

    state.Hook = createHook('click', menuClick)

    function EditorHook() {}
    EditorHook.prototype.hook = (node) => {
      document.body.scrollTop = 0
      var editor = ace.edit(node)
      editor.$blockScrolling = Infinity
      editor.setAutoScrollEditorIntoView(true)
      editor.setTheme('ace/theme/monokai')

      var session = editor.getSession()
      session.setMode('ace/mode/javascript')
      session.setValue(state.code)
    }

    state.EditorHook = EditorHook
    var sandbox = new Sandbox({
        variables: {
            output: () => document.querySelector('#output'),
            times: (n, fn) => {
                var result = []
                for (var i = 0; i < n; i++) {
                    result.push(fn(i))
                }
                return result
            },
            random: (min, max) => Math.round(Math.random() * (max - min)/min ),
            keyEvent: (fn) => {
                document.addEventListener('keydown', function (e) {
                    e.preventDefault()
                    //console.log(e.keyCode)
                    if (~[37, 38, 39, 40].indexOf(e.keyCode)) {

                        fn(e.keyCode)
                    }
                })
            }
        }
    })
    state.RunHook = createHook('click', (e) => {
        state.canRun = false
        document.querySelector('#output').innerText = ""
        // get code from editor
        var editor = ace.edit('editor')
        // evaluate code
        state.code = editor.getSession().getValue()
        var results = sandbox.evaluate(state.code)
        state.markComplete('problem20')
        update()

    })

    state.ResetHook = createHook('click', (e) => {
        state.canRun = true
        //var editor = ace.edit('editor')
        //editor.getSession().setValue(state.code)
        document.querySelector('#output').innerText = ""
        update()
    })

    return state
  }


  component.render = (state) => {

      return h('.mdl-layout.mdl-js-layout', [
        h('header.mdl-layout__header.mdl-layout--fixed-header', [
            h('.mdl-layout__header-row', [
                h('span.mdl-layout-title', ['JavaScript Training - Problem 20']),
                h('span.mdl-layout-spacer'),
                h('.mdl-navigation', [
                    h('button.mdl-navigation__link.mdl-button.mdl-js-button.mdl-button--fab.mdl-js-ripple-effect', {
                        'link-hook': new state.Hook()
                    }, [
                        h('i.material-icons', ['home'])
                    ]),
                    !state.canRun ? h('button.mdl-navigation__link.mdl-button.mdl-js-button.mdl-button--fab.mdl-js-ripple-effect.mdl-button--colored', {
                        'reset-hook': new state.ResetHook()
                    }, [h('i.material-icons', ['replay'])]) : null,
                    state.canRun ? h('button.mdl-navigation__link.mdl-button.mdl-js-button.mdl-button--fab.mdl-js-ripple-effect.mdl-button--colored', {
                        'run-hook': new state.RunHook(),
                        style: { marginLeft: '15px' }
                    }, [h('i.material-icons', ['play_arrow'])]) : null
                ]),
            ])
        ]),
        h('main', [
          h('div.row', [
          h('.col-xs', [
            h('div#editor', { 'editor-hook': new state.EditorHook(), style: { height: '800px', width: '100%' }})
          ]),
          h('.col-xs', [
            h('#output', { style: { margin: '20px'}}, [
              h('h1', 'Snake Game')
            ]),
            h('', { innerHTML: marked(`#### Create a snake game

Next thing we need to do is reset game when rule is broken and eat food:

TODO: Step 1 - reset game if snake its border or itself

    if (
        head.x === -1 ||
        head.y === -1 ||
        head.x === w/size ||
        head.y === h/size
    ) {
        init()
        return
    }

TODO: Step 2 - eat food

    if (head.x === food.x && head.y === food.y) {
        var tail = { x: head.x, y: head.y }
        // TODO 4 increment score when snake eats food
        food = createFood()
    } else {
        var tail = snake.pop()
        tail.x = head.x
        tail.y = head.y
    }

TODO: Step 3 - declare score varable

    var score = 0

TODO: Step 4 - increment score when snake eats food

    score += 1

TODO: Step 5 - reset score

    score = 0

TODO: Step 6 - paint score

    ctx.fillText('Score: ' + score, 5, h - 5)

            `)}),
            h('a', { href: '#', 'link-hook': new state.Hook() }, ['index'])
          ])
        ])
      ])
    ])
  }

  return component
}

function createHook (event, fn) {
    function Hook () { }
    Hook.prototype.hook = (node) => node.addEventListener(event, fn)
    Hook.prototype.unhook = (node) => node.removeEventListener(event, fn)   

    return Hook
}
