# sp-engine
A custom mini programming language engine built in HTML by SHIVANSH PANDEY
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SP Language Engine (Python Powered) - By Shivansh Pandey</title>
    
    <!-- PyScript CSS & JS (Jo browser mein Python chalata hai) -->
    <link rel="stylesheet" href="https://pyscript.net" />
    <script type="module" src="https://pyscript.net"></script>

    <style>
        body { font-family: sans-serif; background: #121212; color: #fff; padding: 20px; max-width: 700px; margin: auto; }
        h1 { color: #00e676; }
        textarea { width: 100%; height: 180px; background: #1e1e1e; color: #00ff88; font-family: monospace; font-size: 16px; padding: 10px; border: 1px solid #333; border-radius: 5px; box-sizing: border-box; }
        button { background: #00e676; color: #000; font-weight: bold; border: none; padding: 12px 24px; font-size: 16px; border-radius: 5px; cursor: pointer; margin-top: 10px; }
        button:hover { background: #00c853; }
        #output { background: #000; color: #fff; padding: 15px; margin-top: 15px; border-radius: 5px; min-height: 80px; font-family: monospace; white-space: pre-wrap; border: 1px solid #333; }
        footer { margin-top: 30px; font-size: 13px; color: #888; text-align: center; }
    </style>
</head>
<body>

    <h1>SP Language Engine 🐍🚀</h1>
    <p>Yeh website aapke <b>Python Engine</b> par chalti hai! Neeche apna SP code likhein:</p>

    <textarea id="codeInput"><SP>...
PRINT=AAPKA NAAM KYA HAI?.
PRINT=SWAGAT HAI ANSWER.
PRINT=50*4.
<SP>...</textarea>

    <button py-click="run_sp_code">▶ Run Python Engine</button>

    <h3>Output:</h3>
    <div id="output">Engine load ho raha hai, kripya 2 second intezar karein...</div>

    <footer>
        Created and Owned by <b>Shivansh Pandey</b> (Age 14) | India 🇮🇳
    </footer>

    <!-- YAHAN AAPKA PYTHON CODE CHALEGA -->
    <script type="py">
        from pyscript import document, window

        document.querySelector("#output").innerText = "SP Python Engine Ready! Ab Run dabayein."

        def run_sp_code(event):
            code = document.querySelector("#codeInput").value
            lines = code.split("\n")
            output_text = ""
            answer = ""
            inside_block = False

            for raw_line in lines:
                line = raw_line.strip()
                if line == "<SP>...":
                    inside_block = not inside_block
                    continue
                if not inside_block or line == "":
                    continue

                if line.startswith("PRINT="):
                    content = line[6:]
                    if content.endswith("."):
                        content = content[:-1]

                    if content.endswith("?"):
                        user_reply = window.prompt(content)
                        answer = user_reply if user_reply is not None else ""
                        output_text += f"{content} -> {answer}\n"
                    elif "ANSWER" in content:
                        output_text += content.replace("ANSWER", answer) + "\n"
                    else:
                        try:
                            # Math calculation check
                            result = eval(content, {"__builtins__": None}, {})
                            output_text += str(result) + "\n"
                        except:
                            output_text += content + "\n"

            document.querySelector("#output").innerText = output_text if output_text else "Koi valid <SP>... code nahi mila."
    </script>

</body>
</html>
