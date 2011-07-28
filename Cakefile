fs           = require 'fs'
CoffeeScript = require 'coffee-script'
nodeunit     = require 'nodeunit'
uglify       = require 'uglify-js'

task 'build', 'build the JavaScript files from CoffeeScript source', build = (cb) ->
  source = fs.readFileSync 'src/ipaddr.coffee'
  fs.writeFileSync 'lib/ipaddr.js', CoffeeScript.compile source.toString()

  invoke 'test'
  invoke 'compress'

task 'test', 'run the bundled tests', (cb) ->
  nodeunit.reporters.default.run ['test']

task 'compress', 'uglify the resulting javascript', (cb) ->
  uglifier = uglify.uglify
  ast = uglify.parser.parse(fs.readFileSync('lib/ipaddr.js').toString())
  ast = uglifier.ast_mangle(ast);
  ast = uglifier.ast_squeeze(ast);
  fs.writeFileSync('ipaddr.min.js', uglifier.gen_code(ast));