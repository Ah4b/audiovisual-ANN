void setup(){
	// die Variablen des Systems definieren
	inputType = chooseInput(audio, visual, controller);
	inputTranslator = findMatchingMethod();
	outputType = chooseOutput(audio, visual, kinetic);
	neural_network = findMatchingTopology();
	trainingData[] = loadTrainingModel();
	maxErrorRatio = tryDifferentErrorRatios();
	
	// die Verknüpfungen zwischen Eingang und Ausgang des Systems gestalten
	// das System mit allen Trainingsdaten trainieren, bis Fehlerquotient des Systems 	
	// kleiner als maxErrorRatio ist
	for (int i = 0; i < trainingData.size(); i++){
		while (neural_network.errorRatio < maxErrorRatio){
			neural_network.train(trainingData[i]);
		}
	}
}
void draw() {
	neural_network.readInput(inputType, inputTranslator);
	neural_network.makeDecision();
	neural_network.writeOutput(outputType);
}
