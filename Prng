from collections import defaultdict, deque

def number_to_category(n):
    return 's' if 0 <= n <= 4 else 'b'

def to_range_0_9(n):
    return int(n) % 10

def get_max_streak(history, mark):
    max_streak = count = 0
    for h in history:
        if h == mark:
            count += 1
            max_streak = max(max_streak, count)
        else:
            count = 0
    return max_streak

# ==== PRNG FORMULAS ====
def formula_1(seq): return to_range_0_9(seq[-1] + seq[-2])
def formula_2(seq): return to_range_0_9(seq[-1] * 3 + 1)
def formula_3(seq): return to_range_0_9(seq[-2] * 2 - seq[-3])
def formula_4(seq): return to_range_0_9(seq[-3] + seq[-1] - seq[-2])
def formula_5(seq): return to_range_0_9((seq[-1] ^ seq[-2]) + 4)
def formula_6(seq): return to_range_0_9((seq[-1] * seq[-2]) + seq[-3])
def formula_7(seq): return to_range_0_9((seq[-1] + seq[-2] + seq[-3]) // 2)
def formula_8(seq): return to_range_0_9(abs(seq[-1] - seq[-2]) + 1)
def formula_9(seq): return to_range_0_9((seq[-1] + 5) ^ seq[-2])
def formula_10(seq): return to_range_0_9((seq[-2] * 3) ^ (seq[-3] + 1))
def formula_11(seq): return to_range_0_9(seq[-3] * 2 + seq[-1])
def formula_12(seq): return to_range_0_9((seq[-1] * 2 - seq[-2]) % 10)
def formula_13(seq): return to_range_0_9((seq[-1] ** 2 + seq[-2]) % 10)
def formula_14(seq): return to_range_0_9((seq[-3] + seq[-2] - seq[-1]) * 2)
def formula_15(seq): return to_range_0_9((seq[-1] + 7) % 10)
def formula_16(seq): return to_range_0_9((seq[-2] - seq[-3]) + 3)
def formula_17(seq): return to_range_0_9(seq[-1] ^ (seq[-2] + seq[-3]))
def formula_18(seq): return to_range_0_9((seq[-1] * 4 + seq[-2]) % 10)
def formula_19(seq): return to_range_0_9(seq[-1] + seq[-2] + seq[-3])
def formula_20(seq): return to_range_0_9((seq[-3] - seq[-2]) * 2)
def formula_21(seq): return to_range_0_9((seq[-2] + 9) % 10)
def formula_22(seq): return to_range_0_9((seq[-1] * 2 + 5) % 10)
def formula_23(seq): return to_range_0_9((seq[-2] ^ 3) + seq[-1])
def formula_24(seq): return to_range_0_9((seq[-3] + 1) * 3)
def formula_25(seq): return to_range_0_9((seq[-1] - seq[-2]) ^ seq[-3])

formulas = [
    formula_1, formula_2, formula_3, formula_4, formula_5,
    formula_6, formula_7, formula_8, formula_9, formula_10,
    formula_11, formula_12, formula_13, formula_14, formula_15,
    formula_16, formula_17, formula_18, formula_19, formula_20,
    formula_21, formula_22, formula_23, formula_24, formula_25
]

# ==== STATE ====
match_history = defaultdict(lambda: deque(maxlen=51))  # For index 0 vs 50
sequence = [1, 2, 3]

# ==== MAIN LOOP ====
while True:
    print("\n🟦 TABLE 1: Predictions")
    predictions = []
    for i, f in enumerate(formulas, 1):
        pred_digit = f(sequence)
        pred_cat = number_to_category(pred_digit)
        predictions.append((i, pred_digit, pred_cat))
        print(f"F{i:02}: Digit = {pred_digit}, Category = {pred_cat}")

    try:
        actual_digit = int(input("\n🎯 Enter ACTUAL digit (0–9): "))
        actual_category = input("🔠 Enter ACTUAL category (s/b): ").strip().lower()
        if actual_digit not in range(10) or actual_category not in ('s', 'b'):
            raise ValueError
    except:
        print("Invalid input. Try again.")
        continue

    sequence.append(actual_digit)

    print("\n🟨 TABLE 2: Comparison Results")
    for i, (fid, pd, pc) in enumerate(predictions):
        result = '✅' if pc == actual_category else '❌'
        match_history[fid].append(result)
        print(f"F{fid:02}: Pred = {pc}, Actual = {actual_category} → {result}")

    print("\n🟩 TABLE 3: Match History Summary")
    for i in range(1, 26):
        hist = list(match_history[i])
        acc = hist.count('✅') / len(hist) * 100 if hist else 0
        max_streak_correct = get_max_streak(hist, '✅')
        max_streak_wrong = get_max_streak(hist, '❌')
        suggestion = 'flip' if acc < 50 else 'straight'
        print(f"F{i:02}: Acc={acc:.1f}% | ✅Max={max_streak_correct} ❌Max={max_streak_wrong} | Suggest: {suggestion} | Hist: {''.join(hist)}")

    print("\n🟥 TABLE 4: 🦖 vs 🎯 Pattern (Index 0 vs 50) + Match Hist")
    for i in range(1, 26):
        hist = list(match_history[i])
        if len(hist) >= 51:
            symbol = '🦖' if hist[0] == hist[50] else '🎯'
            print(f"F{i:02}: Symbol = {symbol} (Index 0 vs 50) | Hist = {''.join(hist)}")
        else:
            print(f"F{i:02}: Not enough history (need 51) | Current length = {len(hist)}")
