import re

# Token specifications
TOKEN_SPECIFICATION = [
    ('KEYWORD',    r'\b(int|float|if|else|while|return)\b'),
    ('IDENTIFIER', r'\b[a-zA-Z_][a-zA-Z_0-9]*\b'),
    ('NUMBER',     r'\b\d+\b'),
    ('OPERATOR',   r'[+\-*/=]'),
    ('SEPARATOR',  r'[;,(){}]'),
    ('SKIP',       r'[ \t\n]+'),
    ('MISMATCH',   r'.'),
]

def lexical_analyzer(code):
    tokens = []
    regex = '|'.join(f'(?P<{name}>{pattern})' for name, pattern in TOKEN_SPECIFICATION)

    for match in re.finditer(regex, code):
        kind = match.lastgroup
        value = match.group()

        if kind == 'SKIP':
            continue
        elif kind == 'MISMATCH':
            print(f'Lexical Error: {value}')
        else:
            tokens.append((kind, value))

    return tokens

# Example usage
source_code = "int x = 10;"
result = lexical_analyzer(source_code)

for token in result:
    print(token)
