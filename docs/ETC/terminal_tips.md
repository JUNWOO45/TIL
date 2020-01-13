# zsh tips

```
prompt_context() { 
	# Custom (Random emoji) 
	emojis=("⚡️" "🔥" "🇰" "👑" "😎" "🐸" "🐵" "🦄" "🌈" "🍻" "🚀" "💡" "🎉" "🔑" "🚦" "🌙") 
	RAND_EMOJI_N=$(( $RANDOM % ${#emojis[@]} + 1)) 
	prompt_segment black default "{하고싶은이름} ${emojis[$RAND_EMOJI_N]} "
}

```

출처 : https://fernando.kr/15?category=790197