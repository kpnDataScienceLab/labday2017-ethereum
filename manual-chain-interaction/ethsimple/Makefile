
test.bin test.abi: test.sol
	solc -o . --bin --abi --overwrite $<
clean:
	rm -f *.abi *.bin
